---
layout: page
title: Next steps
bodyclass: project
---

There are many potential next steps for this project. They fall into two categories: 1) improvements to this site; 2) opportunities that leverage the insights of this work.

## Improvements to situating.us

### Fuzzy search
One of my original goals with this work was to implement _fuzzy search_: that is, to allow people to search by a given word, and find documents that matched that _or similar_ words. For example, a search for "rights" should also consider documents that refer to "suffrage".

An advantage of Doc2Vec-based neural nets (TKTKTK: doc2vec page) is that, during the training process, they learn about word similarities. Therefore, the neural net which underpins this already knows that "rights" and "suffrage" are similar words (TKTKTK amount). Therefore, in principle, it should be possible to compute similarity scores between documents and queries that take words' related meanings into account. Of course, making this fast and easy-to-use could be challenging!

(TKTKTK you can see this, if I keep the recoloring)

Ultimately I did not have time to devote to implementing fuzzy search due to the  [challenges of the data pipeline]({% link about/content/data-challenges.md %}).

### A scrollytelling guided tour
One of the challenges of creating a new paradigm for exploring library data is orienting people to how to use it. The video on the front page provides some support, but I'd love to do something like [Ben Schmidt's Hathi Trust guided tour](http://creatingdata.us/datasets/hathi-features/). Being able to walk people through finding ideas in the data, side-by-side with showing them the visualizations, would let me highlight interesting parts to people who never explore the full visualization, while also better preparing those who do.

### Processing newspapers as articles
One of the [data pipeline challenges]({% link about/content/data-challenges.md %}) is the fact that newspapers are digitized as full-page images, but their natural unit of analysis is the article. This means that each newspaper file contains content from several articles, muddying their distinctions. It would be great if the neural net could cluster articles from different papers about [TKTKTK example], but it has trouble doing that when several articles get mixed together. This muddiness also encourages the neural net to cluster different editions of the same newspaper, because it is likely to run a similar set of article types over time (that is, to be formatted around a particular mix or classifieds, local gossip, political news, poetry, etc.). [TKTKTK NY Tribune classifieds]

This could be mitigated by breaking images into articles before processing them, using a tool such as [LayoutParser](https://layout-parser.github.io/), which was informed by Benjamin Lee's work with Chronicling America (the [Newspaper Navigator](https://news-navigator.labs.loc.gov/) project).

### Handling the gensim word limit

[gensim](https://radimrehurek.com/gensim/) can't process sentences of more than 10,000 words. The various filters I used to clean up newspaper text tended to drop punctuation, which means that some files could end up long enough to be truncated.

Processing newspapers as articles would mitigate this risk, since articles will be shorter than full page newspaper content. However, some non-newspaper documents are quite long, even book-length. Rewriting filters to preserve end-of-sentences punctuation and/or breaking up long documents into several shorter ones (tagged with the same document ID) would help.

### Additional user experience testing
Most of the above would require additional user experience testing. [TKTKTK also my word filters if I end up putting them in the front page]

[TKTKTK something about handling Black newspapers]

## New opportunities
  * did you mean
  * OCR correction
  * LC natively providing article-level newspaper files
* algorithmic bias challenges???
