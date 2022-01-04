---
layout: page
title: Data Cleaning
bodyclass: collections
---

> "The act of cleaning data is the act of preferentially transforming data so that your chosen analysis algorithm produces interpretable results."
>
> [Randy Au](https://counting.substack.com/p/data-cleaning-is-analysis-not-grunt)

## Introduction

The goal of data cleaning with this project was to give people new ways of exploring the collection by encouraging the neural net to cluster on _conceptually meaningful content_. For example, a cluster that contains [TODO: zoom to Anthony/Stanton part, possibly linked from an image below] lots of documents about women's suffrage is conceptually meaningful. By contrast, it's not conceptually meaningful to cluster documents because they share the same meaningless strings of characters due to OCR errors. It's somewhat meaningful to cluster different editions of the same newspaper together, because they have the same title and location of publication — but it isn't _helpful_, because it repeats information we already have from Library of Congress metadata.

I created a number of filters to encourage meaningful clustering by suppressing OCR errors, artifacts of the digitization process, and terms that indicated _format_ more than _content_. These are detailed below.

These filters are particular to the needs of my project: a neural net which learns from every token it sees and transforms that into something visualizable. Other projects, with different computational techniques and interpretive goals, may have different data-cleaning needs.

## Filters

### OCR quality
{% include github_link.html link="https://github.com/thatandromeda/lc_etl/blob/59f4f907c2d2899935f6c3b2d934f36ee15051c5/lc_etl/filter_ocr.py" %}

Optical Character Recognition (OCR) is the process of automatically converting a photograph of text into machine-readable text. It's a critical tool in transforming archival holdings into computationally accessible forms. While the text formats of some Library of Congress documents are [crowdsourced](https://crowd.loc.gov/), the vast majority of documents in this data set are [OCRed Chronicling America newspaper pages](https://chroniclingamerica.loc.gov/ocr/).

OCR is not 100% accurate. Its problems are more severe for historical documents, due to degradation of the physical materials, and for documents which were OCRed in early digitization projects, due to improvements in digitization workflows over time. These are [important challenges for Reconstruction-era newspapers](https://repository.library.northeastern.edu/downloads/neu:m043qk202?datastream_id=content) (see "related issues"); unfortunately, ["Chronicling America is one of the messiest sources of text out there"](http://bookworm.benschmidt.org/posts/2015-10-25-Word-Embeddings.html)

The neural net can survive a modest amount of OCR errors. However, as they proliferate, it will use [more and more of its representational power](https://andromedayelton.com/2020/12/11/though-these-be-matrices-yet-there-is-method-in-them/) to distinguish poorly-OCRed from well-OCRed documents, rather than using that power to distinguish interesting information within well-OCRed documents.

The OCR quality filter calculates the percentage of words in the fulltext file that appear in a given dictionary, [per this approach](http://doi.acm.org/10.1145/2595188.2595214). It uses the [spaCy en_core_web_sm](https://spacy.io/models/en#en_core_web_sm) dictionary, because this is fairly large and able to recognize grammatical variant forms of words (e.g. both "stop" and "stops"). It retains documents where at least 62.5% of the tokens are words[^1], following [Lincoln Mullen's work](https://github.com/lmullen/americas-public-bible/blob/28fcc05ff3aea41795c582e9919cf2969108cb89/notebooks/011-ocr-quality.Rmd#L114) on the Chronicling America corpus for [America's Public Bible](https://americaspublicbible.org/). While this seems low &emdash; documents can be nearly 40% nonwords and still retained &emdash; it strikes a balance between throwing out too much usable text and keeping too much unusable text. Even in a world of perfect OCR, we would not expect 100% of the words in the fulltext file to be recognized words; proper nouns and obsolete slang might not appear in the dictionary.

As a side effect, this filter throws out non-English documents (even if accurately OCRed), since most of their words are not English words. This is helpful for the purposes of this project because the algorithm can't effectively infer relationships between documents in different languages; a translation step would be required to incorporate non-English documents and see their relatedness across (rather than just within) languages.

### Frontmatter

### Archival notes

### Transcription attributions

### Non-words

### Locations

## Notes
[^1] Technically, it retains documents where at least 62.5% of a random sample of 400 words over a minimum length are in the dictionary. This produces very similar decisions to checking every word while taking radically less time to compute.
