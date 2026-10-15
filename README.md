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

## Part 1E: Sales over time
- Created a scatter plot of album sales by release date, colored by artist and faceted by country (UK, US, World) in rows.


## Section 2: Exploring sentiment of lyrics
