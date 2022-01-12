---
layout: page
title: About the Content
bodyclass: collections
navigation_weight: 3
---

Some welcoming text.

## Overview of the topic
Nullam quis porttitor purus, eu finibus justo.

## Data selection
The intent of this project is to provide a discovery interface to Reconstruction-era Library of Congress content. For that reason, I cast as wide a net as possible, processing all Library of Congress materials from 1865-1877 which are available in fulltext format.

This includes a wide array of material types. Examples include:
* A program for a [service observing Lincoln's funeral](https://loc.gov/item/rbpe.1770390a) in Vermont;
* Walt Whitman's notes as he [worked through themes in Leaves of Grass](https://loc.gov/item/mss1863001302);
* A book arguing for [women's rights and equality](https://www.loc.gov/item/09028337/).

However, the vast majority of the documents are newspapers from the [Chronicling America](https://chroniclingamerica.loc.gov/) project.

I considered using materials from other time periods _about_ Reconstruction, but decided against it due to two challenges: copyright and metadata.

**Copyright**. Works from after 1926 are not guaranteed to be in the US public domain as of the publication date of this site (2022). This means that most secondary sources analyzing Reconstruction are unavailable for this project. Notably, both W.E.B. Du Bois's (1935) and Eric Foner's (1988) seminal histories of Reconstruction are unavailable, along with many other modern interpretations. However, Lost Cause interpretations were advanced as a political project by groups such as the United Daughters of the Confederacy in the early 1900s; for example, the notorious [Birth of a Nation](https://www.loc.gov/search/?fa=subject:birth+of+a+nation+%28motion+picture%29) came out in 1915. Attempting to include secondary sources about Reconstruction would therefore result in an extremely one-sided slice through the data, due to the 1926 cutoff.

**Metadata**. Subject headers notwithstanding, library metadata is not really designed to answer a question like "what are all the works in this library pertinent to X". Primary sources that are _from_ Reconstruction are not generally _about_ Reconstruction, even if they tell its story in important ways, and therefore won't be included in a subject header query. Subsequent works that are in a sense about Reconstruction may be primarily about something else, and subject headers will only include the latter. Furthermore, there are many subject headers that may relate to Reconstruction. Therefore there isn't a single query, or even a small set of queries, that catch everything I'm looking for. Fundamentally, subject headers serve as a guide for people who are seeking one, or a handful, or even a few dozen works focused on a particular theme, whereas I was seeking tens or hundreds of thousands of documents that had any light to shed. Therefore< I cast a broad net, performing broad-based date-range queries to pull in as much potentially relevant data as possible.

Additionally, as with any data-intensive project, I had to perform a lot of data cleaning to make the available data suitable for my purposes. I detail this in a [separate section]({% link about/content/data-cleaning.md %}).

## Advisory/disclaimer
Sed tristique placerat iaculis. In faucibus sem eget.

## Contact/report
{% include contact.md %}
