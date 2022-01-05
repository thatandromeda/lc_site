---
layout: page
title: About the Project
bodyclass: project
navigation_weight: 2
---

Some welcoming text.

## Why this project?
Nullam quis porttitor purus, eu finibus justo.

## Why this topic?
Duis cursus semper magna, eu eleifend felis ultrices.

## Tech stack
A goal of this project throughout has been to use the simplest tools available which will get the job done, in order to make the site as easy as possible to maintain over time. Core technologies include:

* [Jekyll](https://jekyllrb.com/). Using a static site generator means staying close to HTML and JavaScript, building blocks of the web, and minimizing external dependencies.
* [gensim](https://radimrehurek.com/gensim/). This machine learning library implements [Doc2Vec](https://arxiv.org/abs/1405.4053) (my algorithm of choice for this project). It's fast and widely used with a straightfoward interface. While I researched more modern algorithms like transformers, Doc2Vec is more suitable for processing long documents.
* Python, JavaScript, and shell scripts.
  * Python is a standard language of machine learning projects and lets me use gensim. Most of the back end of the project is in Python.
  * JavaScript is required for interactive content on the web.
  * Shell scripts are jaw-droppingly fast for large-scale text processing. I reached for them when my computational needs were simple enough that I didn't need Python libraries.
* [deepscatter](https://github.com/CreatingData/deepscatter/), a library for visualizing large numbers of points in the browser in a performant way. It's been used for [large-scale cultural heritage visualization](http://creatingdata.us/datasets/hathi-features/). Correspondly, I used [quadfeather](https://github.com/bmschmidt/quadfeather/) to convert CSV files output by my python scripts into [feather files](https://arrow.apache.org/docs/python/feather.html) usable by deepscatter.
* The web site is hosted on [Digital Ocean](https://www.digitalocean.com/). It's incredibly simple (and free) to deploy a Jekyll project here; hosting the data files is also straightfoward and cheap.
* The Unix filesystem. Starting simple, I decided to use the filesystem for content until I had to set up a database, and found I never had to set up a database; relying on LCCNs and relative paths was enough (once I added some tests to clarify and verify my decisions!).

Being filesystem-based meant I was able to use a range of unix tools constantly throughout my development process. These aren't in my repositories (except as shell scripts) because I used them in the context of my work, not to create deliverables, but their bulletproof reliability and [small pieces loosely joined](https://en.wikipedia.org/wiki/Unix_philosophy) nature made many of these workflow tasks a delight. Some of my favorites included:
  * <code>find</code>: with <code>wc -l</code> for file counting; with <code>-mmin</code> for monitoring the throughput of filtering scripts.
  * <code>shuf</code>, when I realized the visualization would do a much better job of showing the overall structure on load if I randomized the order of elements in the CSV, thereby ensuring the first tile's worth of data points cointained representatives from a variety of collections;
  * <code>grep</code>, constantly and for a wide variety of reasons.
  * <code>tail</code>, for watching logfiles during long-running data pipelines.

## Team & acknowledgements
A project of this scope cannot be done without many hands at work.

Foremost I would like to thank **my team**, <!-- TJ and Frances, pending email responses -->.

I'd also like to thank my **fellow researchers**, [Lauren Tilton](http://laurentilton.com/) and [Lincoln Mullen](https://lincolnmullen.com/), for their perspectives on our related-but-different work. Lincoln in particular gave me helpful guidance from his prior experience processing Library of Congress text files.

At the **Library of Congress**, I had help from the LC Labs team and their orbit: Kate Zwaard, Abigail Potter, Meghan Ferriter, Jaime Mears, Laurie Allen, Eileen Jakeway, Tori Scheppele, Khadijah Camp, and especially my day-to-day liaisons Alice Goldfarb and Olivia Dorsey. Susan Garfinkel and Michelle Krowl helped with reference questions. Nicole Saylor, Christa Maher, Nathan Yarasavage, and Robin Butterhof illuminated the workings of various Library of Congress services. Kelley McNabb and Ellis Brachman advised on communications around our [Wall Street Journal coverage](https://www.wsj.com/articles/library-of-congress-looks-to-ai-to-help-users-sift-through-its-collection-11624552197).

The Computing Cultural Heritage in the Cloud [advisory board](https://labs.loc.gov/work/experiments/cchc/) provided useful feedback on draft work, especially Harriet Green with her comments on highlighting liberatory examples.

[Cecily Walker](https://cecily.info/) helped to assemble literature on algorithmic bias in a library context.

[Ben Schmidt](https://benschmidt.org/) was incredibly generous with his time in helping me understand and troubleshoot deepscatter.

## Next steps
* stuff I could do
  * conceptual search
  * scrollytelling/more support for exploration
* stuff people could do
  * did you mean
  * OCR correction
  * ??? make sure this ties into the presentation

## Contact
I am the sole person maintaining this project, and there is no funding for my time after January 2022. Therefore, unfortunately, I cannot provide extensive customer service.

However, pull requests are welcome on GitHub for [this site](https://github.com/thatandromeda/lc_site) or [the data processing pipeline](https://github.com/thatandromeda/lc_etl). You can contact me with brief questions on [Twitter](https://twitter.com/thatandromeda).
