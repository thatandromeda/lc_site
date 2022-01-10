---
layout: page
title: About the Project
bodyclass: project
navigation_weight: 2
---

Some welcoming text.

## Why this project?
As a librarian and software engineer, I'm interested in giving people new and engaging ways of interacting with cultural heritage collections using machine learning. If we had never seen a card catalog, what would we build? I'm particularly interested in facilitating interactions with library materials in contexts where traditional metadata is not available.

In 2017, I prototyped [HAMLET](https://hamlet.andromedayelton.com/), which would become the inspiration for situating.us. At heart, HAMLET is a neural net, trained on a corpus of about 44,000 theses and dissertations from MIT. It uses the [same algorithm as this project]({% link about/project/doc2vec.md %}), Doc2Vec, which infers whether documents have similar meanings and places them close together or far apart accordingly. I used that underlying technology to support several different ways of exploring the data, such as searching for a given thesis title — or uploading a chapter of a work-in-progress — and getting a list of the most conceptually similar theses, or even the contents of their bibliographies as a first-pass literature review.

As is often the case with thesis & dissertation collections, MIT's has solid records of descriptive information like thesis titles, authors, and departments — but there are no subject headers, and it is unlikely there will ever be enough cataloger time available to create them. This means that, using traditional interfaces, it's hard or impossible to find theses related to a document or topic of interest. I wondered if machine learning might open up new options; it did!

While I was pleased with the sometimes-uncanny usefulness of this first attempt, it was unfinished business for me. I had always hoped to make interactive data visualization components; Doc2Vec's outputs of closer or farther documents lend themselves naturally to visual, spatial processing. However, I was unable to do this due to time and skills limitations.

The Computing Cultural Heritage in the Cloud project provided an opportunity to revisit this work, but with more data, more time, and a team with data visualization and user experience skills. I hope that the results are thought-provoking to people who work in, or love, cultural heritage. How would you interact with library documents online if you could do anything?

## Why this topic?
How we tell the story of Reconstruction is critical to how we understand the story of America.

I did not realize at the time that the particular version of Reconstruction I was taught in high school was developed in the early 1900s as an [academic project](https://en.wikipedia.org/wiki/Dunning_School) to paint freed Black people as incapable of self-governance, in the context of an (https://en.wikipedia.org/wiki/Lost_Cause_of_the_Confederacy)[explicit political project] to romanticize the plantation South and de-emphasize the centrality of slavery to the Civil War.[^1] Nor was I taught that there are many other ways to view this same time period. W.E.B. Du Bois emphasizes the agency of freedmen in advocating for better conditions for workers; the importance of Black institutions like schools and churches; and the role of racism and violence in suppressing Black progress and preventing cross-racial solidarity within the working class. Eric Foner focuses on the hotly-contested transformation of economic and political arrangements during the Reconstruction period, arguing that this [unfinished revolution](https://poets.org/poem/let-america-be-america-again) undergirded the civil rights era a century later.

All of these interpretations advance particular claims, and raise particular questions, about core aspects of the American project. What does it mean to be free? How should our economy be arranged? How do people of different races and classes relate to one another, and why? How long and dark a shadow does slavery cast over our history and present, and what does that mean for Black people in America today? For _all_ people in America today? How do we tell and confont — or hide — our own history, and why?

I hope that by assembling primary sources in a novel interface, I invite you to grapple with history's raw materials and find answers, stories, and new questions. I will be.

## Technology
A goal of this project throughout has been to use the simplest tools available which will get the job done, in order to make the site as easy as possible to maintain over time. This meant relying on Unix tools where possible; using a static site generator for the web site; and (mostly) sticking to widely-deployed, well-tested languages and libraries.

[Read more about the technology choices.]({% link about/project/tech.md %})

[TKTKTK neural nets/doc2vec]

## Team & acknowledgements
A project of this scope cannot be done without many hands at work.

Foremost I would like to thank **my team**. Dr. T.J. Jankun-Kelly, Associate Professor of Computer Science & Engineering within the Bagley College of Engineering, Mississippi State University, reviewed literature on data visualization of large collections and provided research-based guidance on how I could handle this collection.   [Frances Botsford](https://switchingprotocols.com/), a product designer focused on building intuitive and beautiful tools and experiences for organizations big and small (currently at Font Awesome), was the user experience strategist. She conducted UX research, wireframed the web site, and implemented the style and much of the interaction design.

I'd also like to thank my **fellow researchers**, [Lauren Tilton](http://laurentilton.com/) and [Lincoln Mullen](https://lincolnmullen.com/), for their perspectives on our related-but-different work. Lincoln in particular gave me helpful guidance from his prior experience processing Library of Congress text files.

At the **Library of Congress**, I had help from the LC Labs team and their orbit: Kate Zwaard, Abigail Potter, Meghan Ferriter, Jaime Mears, Laurie Allen, Eileen Jakeway, Tori Scheppele, Khadijah Camp, and especially my day-to-day liaisons Alice Goldfarb and Olivia Dorsey. Susan Garfinkel and Michelle Krowl helped with reference questions. Nicole Saylor, Christa Maher, Nathan Yarasavage, and Robin Butterhof illuminated the workings of various Library of Congress services. Kelley McNabb and Ellis Brachman advised on communications around our [Wall Street Journal coverage](https://www.wsj.com/articles/library-of-congress-looks-to-ai-to-help-users-sift-through-its-collection-11624552197). Dave Woodward and Krisztina Thatcher provided insights about the development of the [loc.gov API](https://libraryofcongress.github.io/data-exploration/).

The Computing Cultural Heritage in the Cloud [advisory board](https://labs.loc.gov/work/experiments/cchc/) provided useful feedback on draft work, especially Harriet Green with her comments on highlighting liberatory examples.

[Cecily Walker](https://cecily.info/) helped to assemble literature on algorithmic bias in a library context.

[Ben Schmidt](https://benschmidt.org/) was incredibly generous with his time in helping me understand and troubleshoot deepscatter.

I, [Andromeda Yelton](http://andromedayelton.com/), am responsible for the overall concept, the data pipelines, the machine learning work, some of the front end development, and the web site copy. Any errors and omissions are, of course, entirely my own.

## Next steps
As with any large-scale project, it is all too easy to see the things I didn't have time to do. These include making the visualization searchable; building a scrollytelling-style guided tour; additional user experience testing; and various options for improving data handling.

I can also imagine possibilities which put the technology and insights of this work to very different ends, such as human-in-the-loop but AI-powered OCR correction and improved search capacity for the Library of Congress.

[Read more about possible next steps.]({% link about/project/next-steps.md %})

## Contact
{% include contact.md %}

## Notes
[^1]: I wish to thank Black Twitter for making me think about this, and illustrating competing narratives. Occasionally speaking with but mostly listening to these public intellectuals has transformed my understanding of both history and the present, and I thank them for their generosity with their time, knowledge, and ideas.
