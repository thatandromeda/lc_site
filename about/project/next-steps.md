---
layout: page
title: Next steps
bodyclass: project
nav_category: project
---

There are many potential next steps for this project. They fall into two categories: 1) improvements to this site; 2) opportunities that leverage the insights of this work.

## Improvements to situating.us

### Fuzzy search
One of my original goals with this work was to implement _fuzzy search_: that is, to allow people to search by a given word, and find documents that matched that _or similar_ words. For example, a search for "rights" should also consider documents that refer to "suffrage".

An advantage of [Doc2Vec-based neural nets]({% link about/project/doc2vec.md %})  is that, during the training process, they learn about word similarities. Therefore, the neural net which underpins this already knows that "franchise" and "suffrage" are related words.[^1] Therefore, in principle, it should be possible to compute similarity scores between documents and queries that take words' related meanings into account. Of course, making this fast and easy-to-use could be challenging!

Ultimately I did not have time to devote to implementing fuzzy search due to the  [challenges of the data pipeline]({% link about/content/data-cleaning.md %}).

However, I did implement a taste of it, by precomputing scores for a number of interesting words and allowing you to recolor the graph accordingly. For instance, if you zoom in to the [area around the Elizabeth Cady Stanton papers](/explore?xmin=5.29&xmax=5.69&ymin=8.86&ymax=9.26) and recolor by "suffrage", you'll see some dramatic coloration, since women's suffrage was a frequent topic in her writing.[^2]

### A scrollytelling guided tour
One of the challenges of creating a new paradigm for exploring library data is orienting people to how to use it. The video on the front page provides some support, but I'd love to do something like [Ben Schmidt's Hathi Trust guided tour](http://creatingdata.us/datasets/hathi-features/). Being able to walk people through finding ideas in the data, side-by-side with showing them the visualizations, would let me highlight interesting parts to people who never explore the full visualization, while also better preparing those who do.

### Permalinks
It's possible to zoom into a portion of the graph by specifying coordinates as querystrings in the URL. However, it's not possible, when one _has_ zoomed into a portion, to generate a link corresponding to that portion.

### Processing newspapers as articles
One of the [data pipeline challenges]({% link about/content/data-cleaning.md %}) is the fact that newspapers are digitized as full-page images, but their natural unit of analysis is the article. This means that each newspaper file contains content from several articles, muddying their distinctions.

Ideally we'd like to see the neural net creating clusters of articles from different papers about the same topic. For instance, [this cluster](/explore?xmin=0.17&xmax=0.24&ymin=6.45&ymax=6.55) contains a great many annual reports from, or to, legislative sessions. As these reports are long, they tend to take up a substantial portion of their page, making it easier for the newspapers to cluster them, as the page and the article are somewhat similar when articles are long.

However, the neural net has trouble doing that when several articles (which may be on dissimilar topics) get mixed together. This muddiness also encourages the neural net to cluster different editions of the same newspaper, because it is likely to run a similar set of article types over time (that is, to be formatted around a particular mix or classifieds, local gossip, political news, poetry, etc.). For example, there's a dramatic line of [New York Herald issues](/explore?xmin=4.0&xmax=4.2&ymin=-1.3&ymax=-0.3), which turn out to have clustered because they're pages of help wanted/work sought ads. (Themselves a fascinating window into the conditions of people's lives!)

This could be mitigated by breaking images into articles before processing them, using a tool such as [LayoutParser](https://layout-parser.github.io/), which was informed by Benjamin Lee's work with Chronicling America (the [Newspaper Navigator](https://news-navigator.labs.loc.gov/) project).

### Handling the gensim word limit

[gensim](https://radimrehurek.com/gensim/) can't process sentences of more than 10,000 words. The various filters I used to clean up newspaper text tended to drop punctuation, which means that some files could end up long enough to be truncated.

Processing newspapers as articles would mitigate this risk, since articles will be shorter than full page newspaper content. However, some non-newspaper documents are quite long, even book-length. Rewriting filters to preserve end-of-sentences punctuation and/or breaking up long documents into several shorter ones (tagged with the same document ID) would help.

### Highlighting Black newspapers
The Chronicling America collection includes 26 newspapers for Black audiences from 1865-1877, of which 16 had issues with good enough OCR quality to be included in this data set. Letting users filter for these specifically could be an interesting way to highlight Black experiences during the Reconstruction period.

This would be easy enough to implement technically. However, it would present some user experience challenges. First, adding features without overwhelming or confusing users requires care. Second, the context of these newspapers is important. Some were published by [Black people who had](https://chroniclingamerica.loc.gov/lccn/sn83025783/) [long lived in the regions their papers served](https://chroniclingamerica.loc.gov/lccn/sn84020151/); others were published by [white Northern missionaries or abolitionists who moved south after the war](https://chroniclingamerica.loc.gov/lccn/sn83025784/). Speaking to Black audiences is not the same as speaking from Black perspectives.

### Additional user experience testing
Most of the above would require additional user experience testing.

It would also be interesting to train a variety of neural nets, using different [data filtering options]({% link about/content/data-cleaning.md %}) and [neural net parameters]({% link about/project/doc2vec.md %}), and test them with both novice and expert historians to see which best allowed people to find interesting connections.

## New opportunities
The prior ideas pertain to this web site itself. However, the underlying neural net can be applied to various goals. Furthermore, various projects might improve the neural net's ability to support insights.

### Improved search and "did you mean...?"
When users search the [Library of Congress collections](https://www.loc.gov), or any web site, sometimes they inadvertently enter typos. Alternatively, they may enter the correct word, but the text being searched contains misspellings due to OCR errors, and therefore their search doesn't find the results that it should.

Because the [underlying neural net]({% link about/project/doc2vec.md %}) learns about word similarities, it could be helpful in identifying alternate search terms. This might cover near-synonyms, like suggesting "franchise" to people who search for "suffrage". However, the neural net particularly shines in identifying common typos or OCR errors. For instance, it learns that "suffrago" and "suffrage" are very similar.[^3]

Incorporating a neural net like this one into a search process would let a library web site suggest alternatives to users who had misspelled something. However, there are simpler technologies available to that. The neural net could particularly shine in helping users search across a collection rife with errors, by supplying a variety of alternate terms the search algorithm should also check, including ones that aren't in any dictionary but are common in the underlying collections. For example, as of this writing, there are [1,634 hits for "suffrago" in the Library of Congress](https://www.loc.gov/search/?q=suffrago), all of which users likely hope to surface when they search for "suffrage".

### Semi-automated OCR correction
That said, wouldn't it be better if — instead of modifying searches to correct for OCR errors — the fulltext were accurate in the first place? This would support not only search but any kind of computational project on this corpus.

OCR is notoriously difficult, especially on historical documents. However, a neural net familiar with common OCR errors could provide suggestions of similarly-spelled but legitimate words. I did this in a fully automated fashion in one of my [data filters]({% link about/content/data-cleaning.md %}). It would be more time-consuming, but more accurate, to build this into a [human-in-the-loop interface](https://labs.loc.gov/work/experiments/humans-loop/) that let humans rapidly accept or reject automated suggestions in order to clean data at scale.

## Notes
[^1]: Their relatedness is `0.71` in the neural net underlying this project. In  my experience, anything above `0.65` or so is potentially related enough to be interesting.

Similarly, the model knows that "agriculture" and "horticulture" are similar (`0.79`). It's also excellent at identifying common typos or OCR errors (the similar-looking "farming" and "fanning" have a similarity of `0.82`).

[^2]: You might reasonably ask why the Elizabeth Cady Stanton papers, which largely date to 1848 (the year of the Seneca Falls Convention on women's rights), are in this data set. My guess is that because the dates of her _collected_ papers overlap with my date range of interest (1865-1877), the Library of Congress API returned all of them. This illustrates the challenges of working with large-scale data pipelines!

[^3]: Assuming, of course, that you have not filtered these OCR errors out of your training corpus. I did that for situating.us, so that the neural net could use its powers to find connections among real words rather than to sort out mistakes — but if your goal was to provide suggestions or fix OCR errors, you'd want to leave them all in the training corpus, so that the neural net could learn about misspelled words specifically.
