* The goal was to select everything that was about Reconstruction from the Library of Congress, and nothing that wasn't
* Because of a [variety of challenges]({% link about/content/data-cleaning.md %}), I cast my net as wide as possible for primary sources, then filtered out unusable items.
* The resulting data set included the following (in all cases limited to materials available in online text/OCRed format; <a href="https://github.com/thatandromeda/lc_etl/blob/main/dataset.py">specifics here</a>):
  * All Reconstruction-era Library of Congress digital collections which included online text;
  * Reconstruction-era Supreme Court reports and statutes;
  * Date-filtered queries for a variety of subjects, collections, and contributors, on the advice of Library of Congress reference librarians.
  * All Reconstruction-era Chronicling America content.

  Challenge: copyright

    Cannot include in-copyright works in the neural net training
    Only works published before 1926 are guaranteed to be in the public domain in the US
    This means that many <i>secondary sources</i> are unavailable for this project
    In particular, du Bois' <i>Black Reconstruction in America</i> and Foner's <i>Reconstruction</i> are both unavailable, along with any other modern interpretations
    However, public domain works <i>do</i> include a contemporary-through-early-20th-century project to cast Reconstruction as a tumultuous time and Black Americans as unfit for political power
    Therefore, the secondary sources available represent a particularly biased sample
    <b>Therefore</b> I focus on primary sources

  Challenge: metadata

    Subject headers notwithstanding, library metadata is not really designed to answer a question like "what are all the works in this library pertinent to X"
    Primary sources that are <i>from</i> Reconstruction are not generally <i>about</i> Reconstruction, even if they tell its story in important ways
    Works that are in a sense about Reconstruction may be more primarily about something else, which is what is encoded in the metadata
    Therefore there isn't a single query, or even a small set of queries, that catch everything I'm looking for
    <b>Therefore</b> I cast a broad net, performing multiple broad-based queries to pull in as much potentially relevant data as possible

  Challenge: data quality

    OCRing historical materials is hard
    For reasons: e.g. degraded paper (bleedthrough from the other side; diminished contrast between paper and ink); variable photography quality in digitization process
    Newspapers also use an array of fonts, not all of which OCR well (notably, fancy title fonts)
    The result is that you get things like this (<a href="https://chroniclingamerica.loc.gov/lccn/sn83032011/1871-09-15/ed-1/seq-3/">source</a>):
    <blockquote cite="https://chroniclingamerica.loc.gov/lccn/sn83032011/1871-09-15/ed-1/seq-3/">
      f!m,ITMTAN.
      . .. Ti-!.l a.-l 1K 1071
      AniTIR 1 I I I' . J.11U.1.VI UU )l 1U1 w
      ilvu. 1. linwF.i.i.y"..'' it!:.-VCVi.
      1 ivVriiinii.t. Co., No. 017 Chestnut Ml red,
    </blockquote>
    This problem was acute with newspapers, not so much with non-newspaper items, as they have been through different digitization workflows
    <b>Therefore</b> I filtered the newspapers via the following method, using <a href="https://github.com/lmullen/americas-public-bible/blob/28fcc05ff3aea41795c582e9919cf2969108cb89/chronam/ocr-quality/ocr-quality.go">Lincoln Mullen's strategy</a>, which in turn cites <a href="http://doi.acm.org/10.1145/2595188.2595214">this article</a>:

      Define a dictionary of known good words (I used <code>/usr/share/dict/words</code>) for simplicity
      Count the percentage of words appearing in the OCRed text which also appear in the dictionary
      (In practice, I checked only the first thousand words of any given text, since the checking process is very slow, on the assumption that that is a good proxy for the whole. Texts ranged from 1 to ~21K words.)
      Throw out anything where the percentage is below a cutoff. I used 62.5%, again following Mullen.
      (While this sounds low, the threshold shouldn't be <i>too</i> high. There should be some allowance for imperfect OCR. There are also correctly OCRed words that may not appear in the dictionary, e.g. because they are place names or slang that has gone out of fashion.)

    Challenge: Newspaper clustering

      In the first pass, different editions of the same newspaper ended up clustered together
      I suspect this is because newspapers contain front matter which is the same across editions (e.g. the title and city of publication)
      I don't want newspapers to cluster based on their front matter, though; I want the neural net to examine the content that differs from issue to issue
      A typical newspaper file has 1000+ lines, so cutting a few of them out won't make a huge difference as to content
      <b>Therefore</b> I cut out the first 7 lines of every newspaper file

        To get the number 7, I sampled 100 newspaper files
        Threw out anything that was unreadable due to OCR
        Counted the number of lines at the beginning which were just boilerplate
        Calculated mean, median, 75th, and 95th percentiles
        The mean and 75th percentile were both 4; the vast majority of newspapers had only a handful of lines of boilerplate, if any, but a handful of them spend 35-40 lines talking about advertising rates, circulation policies, etc.
        <b>Therefore</b> I chose th 95th percentile (7 lines), which will eliminate all the boilerplate from the vast majority of newspapers