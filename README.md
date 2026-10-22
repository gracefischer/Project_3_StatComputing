# Project 3
Project 3 for StatComputing Class at BSPH
## Project Breakdown 
Instructions for the project can be found here: https://lcolladotor.github.io/jhustatcomputing/projects/project-3/

## Section 1: Explore album sales
This section uses the TidyTuesday album sales data (September 2020) for Beyoncé and Taylor Swift to practice data wrangling with `stringr`, `lubridate`, and `forcats`, and data visualization with `ggplot2`.

### Part 1A: Data wrangling
- Wrote a regular expression (`" \\([A-Z]+\\)\\[[0-9]+\\]"`) with `stringr::str_remove()` to remove footnote text such as `(US)[51]` from release dates, then converted `released` to a `Date` with `lubridate::mdy()`.
- Converted `country` to a factor with `forcats::fct_collapse()`, combining duplicate levels (`"WW"` and `"World"`, `"FR"` and `"FRA"`).
- Converted `sales` to millions and kept only UK, US, and World sales.

### Part 1B: Years since release (US sales)
- Filtered to US sales and calculated `years_since_release` using `lubridate::interval()` and `floor()` to round down to whole years.
- Summarized the most recent, oldest, and median years since release for each artist.
- Note: values depend on the date the document is rendered because the calculation uses `today()`.

### Part 1C: Sales by country
- Calculated total album sales for each artist and country (UK, US, World).
- Created a percent stacked bar chart showing each country's share of total studio album sales for each artist.

### Part 1D: Worldwide album sales
- Filtered to worldwide sales and created a horizontal bar plot of sales for each album, colored by artist.
- Ordered albums from most to least sales using `forcats::fct_reorder()`.

### Part 1E: Sales over time
- Created a scatter plot of album sales by release date, colored by artist and faceted by country (UK, US, World) in rows.


## Section 2: Exploring sentiment of lyrics
This section uses the Beyoncé and Taylor Swift lyrics datasets to practice text analysis with `tidytext`, including tokenizing text, removing stopwords, and sentiment analysis with the "bing" and "afinn" lexicons.

### Part 2A: "hello" and "goodbye" in Taylor Swift's lyrics
- Split each song in `ts_lyrics` into one row per lyric line with `tidytext::unnest_tokens(token = "lines")`, creating a new `line` column.
- Used `stringr::str_detect()` with `regex(ignore_case = TRUE)` to find lines containing "hello" (6 lines) and "goodbye" (12 lines), and printed all matching rows with `print(n = Inf)`.

### Part 2B: "hello" and "goodbye" in Beyoncé's lyrics
- Repeated Part 2A for `b_lyrics`, which already has one row per line, so no tokenizing step was needed.
- Found 91 lines containing "hello" and 12 containing "goodbye". The high "hello" count comes mostly from the song *Hello* and its live versions.

### Part 2C: Top sentiment words in Beyoncé's lyrics
- Tokenized lyrics into words, removed stopwords with `anti_join(stop_words)`, counted each word, and added "bing" sentiment with `inner_join()`.
- Kept the 25 most frequent words that have a bing sentiment.
- Created a bar plot of word frequency colored by sentiment, with counts labeled at the end of each bar, and a word cloud with the `wordcloud` package.

### Part 2D: Top sentiment words in Taylor Swift's lyrics
- Repeated Part 2C for Taylor Swift's lyrics, starting from the line-level data created in Part 2A.

### Part 2E: Taylor Swift's album sentiment over time
- Counted words by album and added "afinn" sentiment scores (-5 to 5).
- Calculated each album's average sentiment, weighted by how often each word appears.
- Cleaned album names with `stringr::str_trim()` and `str_to_title()` so they matched the sales data, then joined with US sales from Part 1A. *folklore* was dropped because the sales data has no US sales for it.
- Created a scatter plot of average sentiment by release date, sized by US sales in millions, with a horizontal line at 0 (neutral sentiment).
- Found that her earliest albums are the most positive, while later albums are close to neutral, and *1989* is the only album with a negative average.
- Note: the afinn lexicon must be downloaded once through the `textdata` package before rendering.
