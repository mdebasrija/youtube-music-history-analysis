# youtube-music-history-analysis
End-to-end R project to clean Google Takeout data and scrape missing metadata to get a snapshot of my YouTube Music history.

# YouTube Music analytics: 3 years of listening, and the case of the missing metadata

## Project overview

This project processes 43,000+ rows of YouTube Music history from Google Takeout.

### The first hurdle - Not the full history

When I tried to extract my history through the YouTube and YouTube Music option for Takeout, it would give me only a year's worth of history. Sifting through internet forums and blogs proved almost fruitless, until I stumbled on this blog from [Bart Wronski](https://bartwronski.com/2020/01/06/analyze-your-own-activity-data-using-google-takeout/ "Bart Wronski - Analyze your own activity data using Google Takeout"), who suggested using the 'My Activity' history instead of YouTube/YouTube Music. This proved to be much more useful. I got my history until around 2020. Since I wanted to analyse only my YouTube Music data, I extracted that, and that gave me information from 2022 onwards.

### The main challenge - The "Release" artist bug

A significant portion of the Takeout data (\~1,500 rows) had "Release" or `NA` as the artist name. Some of them were because the video was no longer accessible on the internet in India (99 rows). But for the remaining , I developed a custom R scraper to programmatically recover this data.

### The scraper logic

Standard scraping failed due to YouTube's dynamic JavaScript rendering. My solution involved: 1. **URL Transformation:** Pivoting `music.youtube.com` links to standard `www.youtube.com`. 2. **JSON Extraction:** Extracting the hidden `ytInitialPlayerResponse` variable from the page source. 3. **Regex Parsing:** Using string manipulation to find the `shortDescription` and extracting the artist name using the "middle dot" (`·`) delimiter, where the structure is songName (dot) artistName.

## Tools Used

-   **R:** `tidyverse`, `rvest`, `jsonlite`
-   **Visualization:** Tableau

