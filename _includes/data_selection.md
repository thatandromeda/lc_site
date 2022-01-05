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
