# Spotify Data Analysis (Power BI)

![LOGO](https://github.com/KumarBoste/Spotify_Data_Analysis/blob/main/Background/LOGO.webp)

# Spotify Data Analysis – Power BI Project Report

## 1. Project Objective

The objective of this project is to analyze Spotify music data using **Power BI** to uncover meaningful insights about **song performance, artist popularity, and listening trends**. The dashboard is designed to provide a comprehensive, interactive view of Spotify data across three key perspectives: **Overview, Artists, and Songs**. This analysis helps understand content performance, user preferences, and industry trends that can support data-driven decisions in music analytics.



## 2. Problem Statement (Insight-Based)

With the exponential growth of digital music platforms like Spotify, understanding which **artists and songs drive popularity**, how **content is released over time**, and what factors influence **listener engagement** has become increasingly complex. Key challenges addressed in this project include:

* Identifying the most popular artists and songs across the platform
* Understanding trends in song releases by year and month
* Analyzing differences between explicit and non-explicit content
* Comparing performance across album types (single, album, compilation)
* Evaluating song duration and popularity patterns

This project aims to solve these challenges by transforming raw Spotify data into clear, actionable insights using interactive Power BI visualizations.



## 3. Dashboard Sections & Data Visualizations

### A. Overview Dashboard

The **Overview** page provides a high-level summary of Spotify’s music dataset.

**Key Visualizations & Metrics:**

* **Total Songs:** 28K+ songs analyzed
* **Distinct Artists:** 342 unique artists
* **Average Popularity:** 89.62
* **Average Song Duration:** 3.28 minutes
* **Explicit vs Non-Explicit Songs:** Donut chart showing higher presence of non-explicit content
* **Distinct Songs by Album Type:** Albums dominate over singles and compilations
* **Average Popularity by Album Type:** Singles show higher average popularity compared to albums
* **Distinct Songs by Year (2023–2024):** Slight growth in song releases
* **Monthly Popularity Trend:** Line chart showing fluctuations across months
* **Distinct Songs by Month:** Bar chart highlighting peak release months

**Insights:**

* Spotify hosts a vast and diverse music library with strong artist participation
* Singles tend to achieve higher popularity than albums
* Song releases and popularity show seasonal patterns

---

### B. Artists Dashboard

The **Artists** page focuses on artist-level performance and contributions.

**Key Visualizations:**

* **Popularity by Artist:** Bar chart showing top artists such as Taylor Swift, Billie Eilish, and The Weeknd
* **Tracks by Artist:** Average number of tracks per album
* **Songs by Artist:** Count of distinct songs per artist
* **Artist Table:** Includes release date, average popularity, chart position, and average duration

**Insights:**

* A small group of top artists dominate overall popularity
* Artists with fewer releases can still achieve high popularity
* Consistent releases help maintain long-term visibility on the platform

--- 

### C. Songs Dashboard

The **Songs** page provides detailed insights into individual song performance.

**Key Visualizations:**

* **Popularity by Songs:** Ranking of most popular songs
* **Tracks by Songs:** Average track count per album
* **Songs by Songs:** Frequency of song appearances
* **Song-Level Table:** Displays popularity, release date, chart position, and duration

**Insights:**

* Hit songs significantly outperform others in popularity
* Recent releases generally show higher engagement
* Song duration typically ranges between 2–4 minutes, aligning with listener preferences



## 4. Conclusion

The **Spotify Data Analysis Power BI Dashboard** successfully transforms complex music data into meaningful insights. The analysis reveals that:

* Popularity is concentrated among top artists and hit songs
* Singles outperform albums in average popularity
* Seasonal and temporal trends influence song releases and engagement
* Short-to-medium length songs dominate listener preferences

This project demonstrates the effective use of **Power BI for music analytics**, showcasing strong data modeling, visualization, and storytelling skills. It highlights how data-driven insights can support strategic decisions for artists, producers, and streaming platforms.



## 5. Tools & Technologies Used

* **Power BI** – Dashboard creation & data visualization
* **Spotify Dataset** – Music and artist data
* **Data Modeling & DAX** – Measures and calculated insights


## Power BI DAX Query :

``` DAX
DEFINE

    MEASURE 'Top-50-world'[Total Songs] = COUNTROWS('Top-50-world')
    MEASURE 'Top-50-world'[Distinct Songs] = DISTINCTCOUNT('Top-50-world'[song])
    MEASURE 'Top-50-world'[Distinct Artists] = DISTINCTCOUNT('Top-50-world'[artist])
    MEASURE 'Top-50-world'[Avg Popularity] = AVERAGE('Top-50-world'[popularity])
    MEASURE 'Top-50-world'[Max Popularity] = MAX('Top-50-world'[popularity])
    MEASURE 'Top-50-world'[Min Popularity] = MIN('Top-50-world'[popularity])

    MEASURE 'Top-50-world'[Avg Duration Minutes] = AVERAGE('Top-50-world'[duration_ms]) / 60000
    MEASURE 'Top-50-world'[Max Duration Minutes] = MAX('Top-50-world'[duration_ms]) / 60000
    MEASURE 'Top-50-world'[Min Duration Minutes] = MIN('Top-50-world'[duration_ms]) / 60000

    MEASURE 'Top-50-world'[Explicit Songs] = CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[is_explicit] = TRUE())
    MEASURE 'Top-50-world'[Non-Explicit Songs] = CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[is_explicit] = FALSE())
    MEASURE 'Top-50-world'[Pct Explicit Songs] = DIVIDE([Explicit Songs], [Total Songs], 0)
    MEASURE 'Top-50-world'[Avg Popularity Explicit] = CALCULATE(AVERAGE('Top-50-world'[popularity]), 'Top-50-world'[is_explicit] = TRUE())
    MEASURE 'Top-50-world'[Avg Popularity NonExplicit] = CALCULATE(AVERAGE('Top-50-world'[popularity]), 'Top-50-world'[is_explicit] = FALSE())

    MEASURE 'Top-50-world'[Avg Position] = AVERAGE('Top-50-world'[position])
    MEASURE 'Top-50-world'[Position 1 Songs] = CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[position] = 1)
    MEASURE 'Top-50-world'[Position 1 Artists] = CALCULATE(DISTINCTCOUNT('Top-50-world'[artist]), 'Top-50-world'[position] = 1)

    MEASURE 'Top-50-world'[Avg Tracks per Album] = AVERAGE('Top-50-world'[total_tracks])
    MEASURE 'Top-50-world'[Album Type Count] = DISTINCTCOUNT('Top-50-world'[album_type])
    MEASURE 'Top-50-world'[Singles Count] = CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[album_type] = "single")
    MEASURE 'Top-50-world'[Albums Count] = CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[album_type] = "album")

    -- Artist-scoped (use when Artist in context)
    MEASURE 'Top-50-world'[Songs per Artist] = COUNTROWS('Top-50-world')
    MEASURE 'Top-50-world'[Distinct Songs per Artist] = DISTINCTCOUNT('Top-50-world'[song])
    MEASURE 'Top-50-world'[Avg Popularity per Artist] = AVERAGE('Top-50-world'[popularity])
    MEASURE 'Top-50-world'[Position1 Hits per Artist] = CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[position] = 1)

    -- Time-scoped (use when Year in context)
    MEASURE 'Top-50-world'[Songs per Year] = COUNTROWS('Top-50-world')
    MEASURE 'Top-50-world'[Avg Popularity per Year] = AVERAGE('Top-50-world'[popularity])
    MEASURE 'Top-50-world'[Avg Duration per Year] = AVERAGE('Top-50-world'[duration_ms]) / 60000
    MEASURE 'Top-50-world'[Pct Explicit per Year] = DIVIDE(
        CALCULATE(COUNTROWS('Top-50-world'), 'Top-50-world'[is_explicit] = TRUE()),
        [Songs per Year], 
        0
    )

EVALUATE

    SUMMARIZECOLUMNS(
        "Total Songs", [Total Songs],
        "Distinct Songs", [Distinct Songs],
        "Distinct Artists", [Distinct Artists],
        "Avg Popularity", [Avg Popularity],
        "Max Popularity", [Max Popularity],
        "Min Popularity", [Min Popularity],
        "Avg Duration Minutes", [Avg Duration Minutes],
        "Max Duration Minutes", [Max Duration Minutes],
        "Min Duration Minutes", [Min Duration Minutes],
        "Explicit Songs", [Explicit Songs],
        "Non-Explicit Songs", [Non-Explicit Songs],
        "Pct Explicit Songs", [Pct Explicit Songs],
        "Avg Popularity Explicit", [Avg Popularity Explicit],
        "Avg Popularity NonExplicit", [Avg Popularity NonExplicit],
        "Avg Position", [Avg Position],
        "Position 1 Songs", [Position 1 Songs],
        "Position 1 Artists", [Position 1 Artists],
        "Avg Tracks per Album", [Avg Tracks per Album],
        "Album Type Count", [Album Type Count],
        "Singles Count", [Singles Count],
        "Albums Count", [Albums Count],
        "Songs per Artist", [Songs per Artist],
        "Distinct Songs per Artist", [Distinct Songs per Artist],
        "Avg Popularity per Artist", [Avg Popularity per Artist],
        "Position1 Hits per Artist", [Position1 Hits per Artist],
        "Songs per Year", [Songs per Year],
        "Avg Popularity per Year", [Avg Popularity per Year],
        "Avg Duration per Year", [Avg Duration per Year],
        "Pct Explicit per Year", [Pct Explicit per Year]
    )
```

