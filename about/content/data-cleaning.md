---
layout: page
title: Data Cleaning
bodyclass: collections
---

> "The act of cleaning data is the act of preferentially transforming data so that your chosen analysis algorithm produces interpretable results."
>
> <cite>[Randy Au](https://counting.substack.com/p/data-cleaning-is-analysis-not-grunt)</cite>

## Introduction

The goal of data cleaning with this project was to give people new ways of exploring the collection by encouraging the neural net to cluster on _conceptually meaningful content_. For example, a cluster that contains [lots of documents about women's suffrage](/explore.html?xmin=5.55&xmax=5.65&ymin=18.365&ymax=18.45) is conceptually meaningful. By contrast, it's not conceptually meaningful to cluster documents because they share the same meaningless strings of characters due to OCR errors. It's somewhat meaningful to cluster different editions of the same newspaper together, because they have the same title and location of publication — but it isn't _helpful_, because it repeats information we already have from Library of Congress metadata.

I created a number of filters to encourage meaningful clustering by suppressing OCR errors, artifacts of the digitization process, and terms that indicated _format_ more than _content_. These are described below, with links to source code. They are shell scripts where possible, due to the lightning-fast performance of UNIX tools, and Python scripts where they require complex calculation or integration with other Python scripts (external tools or other parts of my codebase).

These filters are particular to the needs of my project: a neural net which learns from every token it sees and transforms that into something visualizable. Other projects, with different computational techniques and interpretive goals, may have different data-cleaning needs.

## Filters

### OCR quality
{% include github_link.html link="https://github.com/thatandromeda/lc_etl/blob/59f4f907c2d2899935f6c3b2d934f36ee15051c5/lc_etl/filter_ocr.py" %}

Optical Character Recognition (OCR) is the process of automatically converting a photograph of text into machine-readable text. It's a critical tool in transforming archival holdings into computationally accessible forms. While the text formats of some Library of Congress documents are [crowdsourced](https://crowd.loc.gov/), the vast majority of documents in this data set are [OCRed Chronicling America newspaper pages](https://chroniclingamerica.loc.gov/ocr/).

OCR is not 100% accurate. Its problems are more severe for historical documents, due to degradation of the physical materials, and for documents which were OCRed in early digitization projects, due to improvements in digitization workflows over time. These are [important challenges for Reconstruction-era newspapers](https://repository.library.northeastern.edu/downloads/neu:m043qk202?datastream_id=content) (see "related issues"); unfortunately, ["Chronicling America is one of the messiest sources of text out there"](http://bookworm.benschmidt.org/posts/2015-10-25-Word-Embeddings.html)

> f!m,ITMTAN.
>
> . .. Ti-!.l a.-l 1K 1071
> AniTIR 1 I I I' . J.11U.1.VI UU )l 1U1 w
>
> ilvu. 1. linwF.i.i.y"..'' it!:.-VCVi.
>
> 1 ivVriiinii.t. Co., No. 017 Chestnut Ml red,
>
> <cite>[The Columbian, September 15, 1871, Image 3](https://chroniclingamerica.loc.gov/lccn/sn83032011/1871-09-15/ed-1/seq-3/)</cite>


The neural net can survive a modest amount of OCR errors. However, as they proliferate, it will use [more and more of its representational power](https://andromedayelton.com/2020/12/11/though-these-be-matrices-yet-there-is-method-in-them/) to distinguish poorly-OCRed from well-OCRed documents, rather than using that power to distinguish interesting information within well-OCRed documents.

The OCR quality filter calculates the percentage of words in the fulltext file that appear in a given dictionary, [per this approach](http://doi.acm.org/10.1145/2595188.2595214). It uses the [spaCy en_core_web_sm](https://spacy.io/models/en#en_core_web_sm) dictionary, because this is fairly large and able to recognize grammatical variant forms of words (e.g. both "stop" and "stops"). It retains documents where at least 62.5% of the tokens are words[^1], following [Lincoln Mullen's work](https://github.com/lmullen/americas-public-bible/blob/28fcc05ff3aea41795c582e9919cf2969108cb89/notebooks/011-ocr-quality.Rmd#L114) on the Chronicling America corpus for [America's Public Bible](https://americaspublicbible.org/). While this seems low — documents can be nearly 40% nonwords and still retained — it strikes a balance between throwing out too much usable text and keeping too much unusable text. Even in a world of perfect OCR, we would not expect 100% of the words in the fulltext file to be recognized words; proper nouns and obsolete slang might not appear in the dictionary.

As a side effect, this filter throws out non-English documents (even if accurately OCRed), since most of their words are not English words. This is helpful for the purposes of this project because the algorithm can't effectively infer relationships between documents in different languages; a translation step would be required to incorporate non-English documents and see their relatedness across (rather than just within) languages.

### Frontmatter
{% include github_link.html link="https://github.com/thatandromeda/lc_etl/blob/59f4f907c2d2899935f6c3b2d934f36ee15051c5/lc_etl/bulk_scripts/remove_frontmatter.sh" %}

Newspapers frequently have repetitive content in their first few lines. Very often, this includes titles and locations of publication; sometimes it also includes the name of the publisher, subscription policies, or advertisement policies. The neural net will learn this unvarying content and cluster files together on its basis, thereby placing different issues of the same newspaper together regardless of article content.

Because I want to encourage the neural net to cluster based on article content — that is, I'd rather see a cluster composed of articles on one topic from a variety of newspapers than articles from one newspaper on a variety of topics — I delete that frontmatter.

By randomly sampling a hundred newspapers and counting their lines of boilerplate, I concluded that removing the first 10 lines of a file will remove this boilerplate in the vast majority of cases, while still leaving the vast majority of text intact for analysis. The remaining cases have several dozen lines of boilerplate content (for example, [J.L. Boardman's enthusiasm](https://chroniclingamerica.loc.gov/lccn/sn85038158/1868-08-20/ed-1/seq-1/) in describing payment and delivery policies for the Highland Weekly News (Hillsboro, Ohio).)

### Archival notes
{% include github_link.html link="https://github.com/thatandromeda/lc_etl/blob/59f4f907c2d2899935f6c3b2d934f36ee15051c5/lc_etl/bulk_scripts/remove_archival_notes_gentle.sh" %}

Some original paper documents — for instance, in the [Charles E. Feinberg's collection of Walt Whitman's papers](https://www.loc.gov/collections/feinberg-whitman/about-this-collection/) — are stored within folders, which are labeled, and may also contain pages with archival notes. When the Whitman papers were digitized, they were photographed in their entirety (folders, notes, and originals); these images were then transcribed via crowdsourcing to create the fulltext document, and the fulltext consists of the concatenation of all images for an item. The result is that the fulltext file may contain folder labels and archival processing notes in addition to the original text (for example, in [these notes on Leaves of Grass](https://www.loc.gov/resource/mss18630.04036/)).

Transparency about archival processing is important to the historical record. However, as these notes are not original Reconstruction-era content, I attempted to exclude them from my analysis. Whenever I detected the "Box X Folder Y" pattern, I deleted the first 10 lines of the document. This is often enough to exclude the archival notes without treading too harshly on the remaining content. Unfortunately, as archivists' notes may be interfiled with original documents, removing the beginning of a file doesn't reliably exclude them. Because these notes are variable in form and content, it's not possible to write a script which recognizes and surgically removes only this part of the file.

I also created, though did not end up using, a [harsh version](https://github.com/thatandromeda/lc_etl/blob/59f4f907c2d2899935f6c3b2d934f36ee15051c5/lc_etl/bulk_scripts/remove_archival_notes_harsh.sh) of this script which simply deletes any documents with the "Box X Folder Y" pattern.

### Transcription attributions
{% include github_link.html link="https://github.com/thatandromeda/lc_etl/blob/59f4f907c2d2899935f6c3b2d934f36ee15051c5/lc_etl/bulk_scripts/remove_transcription_attribution.sh" %}

Documents that have been [crowdsourced](https://crowd.loc.gov/) rather than OCRed include a line recognizing volunteers for their work. While this recognition is appropriate, it introduces anachronistic content into the fulltext file, and encourages the neural net to cluster documents based on their transcription method rather than their content (by learning this line and clustering documents that share it).

Luckily, this line is identical wherever it appears, so it is easy to identify and delete.

### Non-words
{% include github_link.html link="https://github.com/thatandromeda/lc_etl/blob/59f4f907c2d2899935f6c3b2d934f36ee15051c5/lc_etl/filter_nonwords.py" %}

As noted above, the neural net will use a lot of its learning capacity on [recognizing OCR errors](https://andromedayelton.com/2020/12/11/though-these-be-matrices-yet-there-is-method-in-them/) if they are common. In addition, a corpus with a lot of errors will have a huge number of distinct words that the neural net has to process, because a single word may appear as a range of errors (e.g. "very" vs. "▼ery").

It would be nice to be able to automatically replace these errors with their originally intended versions. I hypothesize that an error E probably represents an original word O if the following are true:
1. E and O are similar in meaning;
2. E and O don't differ by too many characters (as, for example, "very" vs. "▼ery" are only one character apart).

These are things I can measure! I use an intermediate neural net, trained on a subset of my full corpus, to measure word similarity. If "▼ery" occurs enough times in this subset, the neural net will learn that it appears in contexts similar to those that "very" appears in. I use the popular [Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance) to measure the difference between characters (1, in the case of "very" vs. "▼ery").

The nonwords filter replaces a nonword when it can find a suitable candidate, using the above measurements with moderately permissive thresholds. When it can't find a suitable replacement, it drops the word.

This creates a corpus that is probably similar to the original intent where possible, but consisting only of recognized words. This sacrifices some accuracy in corpus representation (some of the "corrected" words will be wrong; perfectly valid proper nouns not in the dictionary are dropped). In exchange, it gains some accuracy (by correcting words correctly) and yields a radically smaller overall corpus vocabulary (by dropping or replacing nonwords), resulting in much faster neural net training with much lower memory requirements. This, in turn, facilitates experimenting with a wider variety of neural net hyperparameters.

I postprocessed the entire corpus (remaining after the above filters) with this filter.

### Locations
{% include github_link.html link="https://github.com/thatandromeda/lc_etl/blob/59f4f907c2d2899935f6c3b2d934f36ee15051c5/lc_etl/filter_newspaper_locations.py" %}

I also hypothesize that newspapers are quite likely to contain their own titles and locations throughout their text (as they comment on local news), and this will push the neural net toward clustering on those words and away from clustering on other concepts. That is, I'd prefer that elections-oriented content end up together across a variety of local elections than for local news on a variety of topics to end up together because it's local.

Therefore I use Library of Congress metadata on titles and locations to remove matching words. This is an extremely incomplete filter since the filter considers documents one word at a time and many place names are two words (e.g. Des Moines, New Haven, Baton Rouge, Chester County).

## Notes
[^1]: Technically, it retains documents where at least 62.5% of a random sample of 400 words over a minimum length are in the dictionary. This produces very similar decisions to checking every word while taking radically less time to compute.
