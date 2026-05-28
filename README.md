# Investigating 1990s Movies 🎬

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=flat-square)
![Seaborn](https://img.shields.io/badge/Seaborn-4c72b0?style=flat-square)

---

This is a personal project, built as a playground for practicing data exploration and visualization techniques. The goal was never just to answer questions about 90s movies — it was to use a fun dataset as an excuse to experiment with chart choices, visual storytelling, and how different tools handle the same data differently.

The dataset is `netflix_data.csv`, filtered to movies released between 1990 and 1999. The questions came from the data. The real exercise was deciding how to show the answers.

---

## ✦ The Dataset

The dataset contains Netflix movie records with the following columns used in this analysis:

| Column | Description |
|--------|-------------|
| `title` | Movie title |
| `type` | Content type (filtered to "Movie") |
| `release_year` | Year of release |
| `country` | Country of production |
| `listed_in` | Genres |
| `director` | Director name |
| `duration` | Runtime in minutes |
| `description` | Movie description |

<br/>

## ✦ 1. Release Trends Over the Decade

The first question was simple: how many movies were released each year? A **line chart** was the natural choice here — we're looking at a continuous trend over time, and lines make it easy to spot direction and inflection points.

```python
movies_per_year = movies_90s.groupby('release_year').size()

plt.figure(figsize=(10, 5))
sns.lineplot(data=movies_per_year, marker='o')
plt.title('Number of Movies Released (1990–1999)')
plt.xlabel('Year')
plt.ylabel('Number of Movies')
plt.show()
```

Releases showed a steady upward trend, with a noticeable jump between 1996 and 1997. That could reflect technology shifts, broader streaming cataloging, or simply more content being produced globally in that period.

<img src="https://drive.google.com/uc?id=1EWzXvVPdFjWufq8jqnpQPFD1q6eVB-vu" alt="Number of Movies Released" width="700" />

Breaking it down by country revealed something more interesting. A simple line chart per country would get cluttered fast, so the choice was to filter to the **top 3 producers** and compare them side by side. This keeps the chart readable while still showing regional differences.

<img src="https://drive.google.com/uc?id=10IA4NEvoIglqVAEkA5NyR9SwbeTuMHsk" alt="Movies Released by Country - Top 3" width="700" />

The US led consistently, peaking in 1997. India showed steady growth toward the end of the decade — Bollywood's rise was already happening. The UK contributed meaningfully but at a smaller scale.

<br/>

## ✦ 2. Popular Genres

For genres, a **bar chart** made more sense than a pie chart. Pie charts struggle with more than 4 or 5 categories, and here we had more than that. Bars make it easy to compare values across many categories at once.

<img src="https://drive.google.com/uc?id=1GYsQgOASpCcFst8gBjuggTiqwz7x64Lb" alt="Popular Genres of the 90s" width="700" />

Action, Drama, and Comedy dominated, not surprising for the 90s. What was interesting was how genre distribution shifted by country. Breaking the same bar chart down by the top 3 producing countries revealed that India leaned heavily into Drama, while the US and UK showed a broader spread across genres.

This is a good example of why aggregated charts can hide patterns: the overall ranking looked one way, but the country-level view told a different story.

<img src="https://drive.google.com/uc?id=11pBDKWGHDMLV3RPl_nMMOxeoBZVYbgYX" alt="Popular Genres by Country" width="700" />

<br/>

## ✦ 3. Directors

Most directors in the dataset released between 1 and 4 movies in the 90s, with an average of 1.24 films per director. No single figure dominated the decade in terms of volume.

```python
top_directors = movies_90s['director'].value_counts().head(10)
top_directors
```

| Director | Number of Films |
|----------|----------------|
| Johnnie To | 4 |
| Youssef Chahine | 3 |
| Umesh Mehra | 3 |
| Gregory Hoblit | 3 |
| Subhash Ghai | 3 |
| Mahesh Bhatt | 3 |
| Rajkumar Santoshi | 3 |
| Sooraj R. Barjatya | 3 |
| David Dhawan | 2 |
| Quentin Tarantino | 2 |

A simple ranked table worked better here than a chart. The values are close enough that a bar chart would not add much visual clarity, and the names themselves carry context that a chart would lose.

<br/>

## ✦ 4. Themes in Titles and Descriptions

To explore recurring themes, I used **word clouds**: one for movie titles, one for descriptions. Word clouds are often criticized for being imprecise, and that criticism is fair. But for this specific use case, the goal was not to rank themes precisely: it was to get a quick visual sense of what language dominated the decade. For that, a word cloud works well.

<img src="https://drive.google.com/uc?id=1LTq4Rn1jJ6M3g0ngtFfq5zwJRQ6xGBHt" alt="Word Cloud - Movie Titles" width="700" />

Titles leaned toward words like "love", "beauty", and "romance", alongside "danger", "mystery", and "fear" — a clear reflection of the emotional range of 90s cinema.

Descriptions reinforced family and coming-of-age themes, with action and adventure also featuring strongly.

<br/>

## ✦ 5. Runtime Distribution

For runtime, I used a **histogram** to show the distribution. When the question is "what does the spread look like?", histograms are the right tool. They show shape, concentration, and outliers better than a simple average or a box plot would in a first pass.

<img src="https://drive.google.com/uc?id=1_xTM9gr2Shi_0sNxHO5ZCLm7btNGQ1cV" alt="Runtime Distribution" width="700" />

Most films landed between 100 and 120 minutes, with an average of 115 minutes. Then I broke runtime down by genre using a **box plot**. The right choice when comparing distributions across multiple categories, since it shows median, spread, and outliers all at once.

<img src="https://drive.google.com/uc?id=1Gm2XxTHsRqIBM22Jl1jT7Nyv79T3SMp3" alt="Runtime by Genre" width="700" />

Action and Drama films tended to run longer. Comedies and family films were consistently shorter, which makes intuitive sense and is also useful context for anyone thinking about content pacing.

<br/>

## ✦ Key Takeaways

This project was less about the 90s and more about practicing intentional visualization choices:

- **Line charts** for trends over time
- **Bar charts** for comparing categories, especially when there are many
- **Word clouds** for a quick thematic overview, not precise ranking
- **Histograms** for understanding distributions
- **Box plots** for comparing distributions across groups
- **Tables** when values are close and labels matter more than visual shape

The dataset was simple enough to focus on the how, not just the what, which was exactly the point.

<br/>

---

<sub>☕︎ Made by <a href="https://github.com/devleticiastahl">Leticia Stahl</a></sub>
