---
layout: page
title: Technology
bodyclass: project
---

Core technologies for this project included:

**[Gensim](https://radimrehurek.com/gensim/).** This machine learning library implements [Doc2Vec](https://arxiv.org/abs/1405.4053) (my algorithm of choice for this project). It's fast and widely used with a straightfoward interface. While I researched more modern algorithms like transformers, Doc2Vec is more suitable for processing long documents.

Doc2Vec, and how neural nets work more generally, demands more attention than I can give it in a paragraph; here's an [in-depth discussion]({% link about/project/doc2vec.md %}).

**[Jekyll](https://jekyllrb.com/).** Using a static site generator means staying close to HTML and JavaScript, building blocks of the web, and minimizing external dependencies.

**Python, JavaScript, and shell scripts.** Python is a standard language of machine learning projects and lets me use gensim. Most of the back end of the project is in Python. JavaScript is required for interactive content on the web. Shell scripts are jaw-droppingly fast for large-scale text processing. I reached for them when my computational needs were simple enough that I didn't need Python libraries.

**[Deepscatter](https://github.com/CreatingData/deepscatter/)**, a library for visualizing large numbers of points in the browser in a performant way, designed in part around the needs of [large-scale cultural heritage visualization](http://creatingdata.us/datasets/hathi-features/). Correspondingly, I used [quadfeather](https://github.com/bmschmidt/quadfeather/) to convert CSV files output by my python scripts into [feather files](https://arrow.apache.org/docs/python/feather.html) usable by deepscatter.

The web site is hosted on **[Digital Ocean](https://www.digitalocean.com/).** It's incredibly simple (and free) to deploy a Jekyll project here; hosting the data files is also straightfoward and cheap.

**Unix**: its filesystem and [philosophy](https://en.wikipedia.org/wiki/Unix_philosophy). I planned to start simple by using the filesystem for content until I outgrew it and needed a database, and then found I never had to set up a database; relying on LCCNs and relative paths was enough (once I added some tests to clarify and verify my decisions!).

Being filesystem-based meant I was able to use a range of unix tools constantly throughout my development process. These aren't in my repositories (except as shell scripts) because I used them in the context of my work, not to create deliverables, but their bulletproof reliability and composable nature made many of these workflow tasks a delight. Some of my favorites included:
  * <code>find</code>: with <code>wc -l</code> for file counting; with <code>-mmin</code> for monitoring the throughput of filtering scripts.
  * <code>shuf</code>, when I realized the visualization would do a much better job of showing the overall structure on load if I randomized the order of elements in the CSV, thereby ensuring the first tile's worth of data points cointained representatives from a variety of collections;
  * <code>grep</code>, constantly and for a wide variety of reasons.
  * <code>tail</code>, for watching logfiles during long-running data pipelines.
