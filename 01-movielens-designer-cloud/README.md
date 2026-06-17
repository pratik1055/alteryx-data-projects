# MovieLens Genre Analysis — Alteryx Designer Cloud

An ETL pipeline that takes the raw MovieLens dataset and answers: **which movie genres are rated highest, and how much rating volume supports each average?**

Built in Alteryx Designer Cloud (formerly Trifacta).

---

## The Data

| File | Rows | Columns |
|---|---|---|
| `movies.csv` | 9,742 | movieId, title, genres (pipe-delimited) |
| `ratings.csv` | 100,836 | userId, movieId, rating, timestamp |
| `tags.csv` | 3,683 | userId, movieId, tag, timestamp |

The challenge: genres are stored as a single pipe-delimited string (e.g. `Adventure|Animation|Children|Comedy|Fantasy`), so they must be split and reshaped before any per-genre analysis is possible.

---

## The Pipeline

1. **Ingest** — load the three CSV files.
2. **Clean & type** — Data Cleanse + Auto Column to standardise and set data types.
3. **Split genres** — Text to Columns on the `|` delimiter, producing up to 10 genre columns.
4. **Unpivot** — Transpose the genre columns into one row per (movie, genre).
5. **Filter** — drop null genre slots (reduced ~97K rows to ~22K real genre assignments).
6. **Conditional column** — bucket each rating into High / Medium / Low.
7. **Join** — inner join the genre-level movies to ratings on `movieId`.
8. **Aggregate** — group by genre; compute average rating and rating count.
9. **Output** — write the genre summary to CSV.

---

## Result

Average rating per genre (top and bottom):

| Genre | Avg Rating | Rating Count |
|---|---|---|
| War | 3.67 | 4,859 |
| Documentary | 3.62 | 1,219 |
| Drama | 3.51 | 41,928 |
| Crime | 3.51 | 16,681 |
| ... | ... | ... |
| Action | 3.29 | 30,635 |
| Comedy | 3.23 | 39,053 |
| Horror | 3.10 | 7,291 |

**Finding:** "Prestige" genres (War, Documentary, Drama, Crime) rate highest, while broad-appeal genres (Horror, Comedy, Action) sit lowest. High-volume genres like Drama and Comedy (~40K ratings each) have the most statistically reliable averages.

---

## SQL Equivalent

The whole pipeline is equivalent to:

```sql
SELECT genre, COUNT(*) AS rating_count, AVG(rating) AS avg_rating
FROM movies
  -- genres split from pipe-delimited string into one row per genre
  JOIN ratings USING (movieId)
GROUP BY genre
ORDER BY avg_rating DESC;
```

---

## Files

- `data/` — raw input CSVs
- `outputs/` — generated CSVs (genre summary + cleaned tables)
- `screenshots/` — the workflow canvas
