---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
title: Home
layout: home
bodyclass: home
navigation_weight: 1
---

<div class="hero">
  <h1 class="home-title">Situating Ourselves<br> in Cultural Heritage</h1>
  <div class="snapshot-wrapper framed">
    <img src="/assets/images/scatter-snapshot.png" alt="Situating US tool screenshot" />
  </div>
</div>

What if you could see the breadth of content across hundreds of thousands of historical documents at a glance? What if a machine could read all of them and help you find your own connections — and your own understanding of America?

This experimental project aimed to use, learn about, and help improve computational access to Library of Congress digital content, and to expose more of the Library's rich collections to scholars and the public. Using machine learning, this exploratory tool serves as a proof of concept for finding potentially similar or related content outside of manual classification. It incorporates all available documents from the Reconstruction era (1865-1877), because how we tell the story of this period is critical to how we understand America.

## Exploring the Collections
As you begin an exploration of the collections, items will scatter across the screen. There are thousands of articles, letters, book chapters, manuscripts, and other text-rich items represented in the display, so some clusters or dots may represent several items; zoom in to see more.

Here’s a short video overview:

<div class="video-wrapper framed">
<iframe width="100%" height="100%" src="https://www.youtube-nocookie.com/embed/jMr9v0t1jNM" title="YouTube video player" frameborder="0" allowfullscreen></iframe>
</div>

The collections included focus on the post-Civil War era of Reconstruction in the United States, and may include challenging material. [Read more about the content.]({% link about/content.md %})

<p><a class="cta-button" href="/explore">Explore the Collections</a></p>

## Where should I start?
You're welcome to dive in anywhere! Zoom and pan with your mouse and use the color-coding options to look for groups with interesting shapes. Then hover or click on the dots to learn more about the documents they represent and look for common themes. Click through to the originals at the Library of Congress to read the full text, which may give you even more insights. I invite you to discover your own meanings in the collection.

Not sure where to start? How about:
* [The women's suffrage movement](/explore/?xmin=5.3&xmax=5.4&ymin=7.3&ymax=7.6), which was contemporaneous with Reconstruction. Both women's suffrage and abolition wrestled with questions of equality, citizenship, and belonging...but with lively debate over whether white women and Black men should fight together or take turns, and with Black women too often excluded. Interesting documents are easier to see here if you color by "suffrage".
* [New York Herald classified ads](/explore/?xmin=13&xmax=14&ymin=12&ymax=13), which provide a window into everyday life.
* News articles, proclamations, and more concerning [how to handle Confederate soldiers and the return to peace after the Civil War](/explore/?xmin=10.3&xmax=11.2&ymin=4.4&ymax=4.6). It's easier to find documents of interest here if you recolor by "constitution".
<!-- * [TKTKTK contains following: https://chroniclingamerica.loc.gov/lccn/sn93067983/1865-07-07/ed-1/seq-4/ , https://chroniclingamerica.loc.gov/lccn/sn83030313/1865-01-26/ed-1/seq-5/ , https://chroniclingamerica.loc.gov/lccn/sn84027007/1865-07-04/ed-1/seq-1/ , https://www.loc.gov/item/rbpe.20406400/ -- all about trying to figure out what to do with soldiers after the War -- coords don't seem to map right to display]
[TKTKTK can't find a good thing with Black newspapers]
the "abolition" spike at 4oclock? -->

Or you can follow along in these videos: 

<div class="example-videos-wrapper">
  <a class="framed" data-micromodal-trigger="modal-1" href='javascript:;'>
    <img src="/assets/images/suffrage-example.jpeg" />
    <span>Watch a video example exploring Women's Suffrage</span>
  </a>
  <a class="framed" data-micromodal-trigger="modal-3" href='javascript:;'>
    <img src="/assets/images/classifieds-example.jpeg" />
    <span>Watch a video example exploring Classified Ads</span>
  </a>
  <a class="framed" data-micromodal-trigger="modal-2" href='javascript:;'>
    <img src="/assets/images/troops-example.jpeg" />
    <span>Watch a video example exploring Civil War Troops</span>
  </a>
</div>

<div class="modal micromodal-slide" id="modal-1" aria-hidden="true">
  <div class="modal__overlay" tabindex="-1" data-micromodal-close>
    <div class="modal__container" role="dialog" aria-modal="true" aria-labelledby="modal-1-title">
      <header class="modal__header">
        <h2 class="modal__title" id="modal-1-title">Exploring by Topic: Women's Suffrage</h2>        
        <button id="closeModal1" class="modal__close" aria-label="Close modal" data-micromodal-close></button>
      </header>
      <main class="modal__content" id="modal-1-content">
        <iframe id="videoSuffrage" width="640" height="390" src="https://www.youtube.com/embed/bvubXvs7wo4?enablejsapi=1" title="YouTube video player" frameborder="0" allowfullscreen></iframe>
      </main>
    </div>
  </div>
</div>

<div class="modal micromodal-slide" id="modal-2" aria-hidden="true">
  <div class="modal__overlay" tabindex="-1" data-micromodal-close>
    <div class="modal__container" role="dialog" aria-modal="true" aria-labelledby="modal-2-title">
      <header class="modal__header">
        <h2 class="modal__title" id="modal-2-title">Exploring by Cluster: Civil War Troops</h2>        
        <button id="closeModal2" class="modal__close" aria-label="Close modal" data-micromodal-close></button>
      </header>
      <main class="modal__content" id="modal-2-content">
        <iframe id="videoTroops" width="640" height="390" src="https://www.youtube.com/embed/tD8h5kIwe8E?enablejsapi=1" title="YouTube video player" frameborder="0" allowfullscreen></iframe>
      </main>
    </div>
  </div>
</div>


<div class="modal micromodal-slide" id="modal-3" aria-hidden="true">
  <div class="modal__overlay" tabindex="-1" data-micromodal-close>
    <div class="modal__container" role="dialog" aria-modal="true" aria-labelledby="modal-3-title">
      <header class="modal__header">
        <h2 class="modal__title" id="modal-3-title">Exploring by Cluster: Classified Ads</h2>        
        <button id="closeModal3" class="modal__close" aria-label="Close modal" data-micromodal-close></button>
      </header>
      <main class="modal__content" id="modal-3-content">
        <iframe id="videoAds" width="640" height="390" src="https://www.youtube.com/embed/DjGoYNyxKFo?enablejsapi=1" title="YouTube video player" frameborder="0" allowfullscreen></iframe>
      </main>
    </div>
  </div>
</div>


<p><a class="cta-button" href="/explore">Try It Out Yourself!</a></p>

Find something interesting? Share it on social media with #SituatingUs.

# About the Collections and Subject Area
The project includes documents in the Library of Congress from the United States, between 1865 and 1877, which have been digitized as full text. This is mostly newspapers from  [Chronicling America](https://chroniclingamerica.loc.gov/), but also includes a wide array of other things, including broadsheets and pamphlets; books; and content from the papers of Abraham Lincoln, Walt Whitman, Elizabeth Cady Stanton, and others. The focus is on the Reconstruction era. [Learn more](/about/content).

{% include disclaimer.html %}

# About the Project
This project is part of the [Computing Cultural Heritage in the Cloud project](https://labs.loc.gov/work/experiments/cchc/) of the [Library of Congress Labs](https://labs.loc.gov/), which aims to increase computational access to collections. [Learn more about the project.](/about/project)
