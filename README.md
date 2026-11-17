# Does Passing the Bechdel Test Pay Off at the Box Office?

**ANOVA and a permutation test on FiveThirtyEight's Bechdel Test data to check whether a film's gross revenue differs by how it treats its female characters.**

![R](https://img.shields.io/badge/R-276DC3?logo=r&logoColor=white)
![Quarto](https://img.shields.io/badge/Quarto-39729E?logo=quarto&logoColor=white)
![tidyverse](https://img.shields.io/badge/tidyverse-1A162D)
![infer](https://img.shields.io/badge/infer-permutation%20test-blue)

Final project for **SDS 220** (introductory statistics) at Smith College, by **Radiah Khan and Bree Gordon**.

---

## Question

A film passes the [Bechdel Test](https://bechdeltest.com/) if it has at least two named women who talk to each other about something other than a man. We asked:

> **Does a movie's total gross income (domestic + international, in 2013 dollars) differ across Bechdel Test outcomes?**

Films are grouped by *why* they pass or fail: they pass; it is dubious; the women only talk about men; the women don't talk to each other; or there are fewer than two women.

## Approach

1. **Wrangling**: combine domestic and international gross (inflation-adjusted to 2013) into one variable, keep the Bechdel outcome and drop films with missing revenue.
2. **Exploration**: revenue distributions for passing vs. failing films and summary statistics (n, mean, SD, min, max) for each outcome.
3. **One-way ANOVA** of gross income on Bechdel outcome.
4. **Permutation test** (1,000 shuffles with `infer`) of the same F-statistic, which doesn't depend on the normality assumption that heavily skewed box-office data violates.
5. **Post-hoc pairwise t-tests** with Bonferroni correction to find which outcomes differ.

## Results

- **Mean gross income differs significantly across Bechdel outcomes**: ANOVA F = 5.90, p = 0.0001.
- The **permutation test agrees**: none of the 1,000 shuffled datasets produced an F-statistic as large as the observed one (p < 0.001). The difference is not an artifact of skewed revenue.
- Bonferroni-adjusted pairwise t-tests follow up on the ANOVA to locate which outcome groups differ from each other.

## Files

| File | Purpose |
|---|---|
| `FINAL_PROJECT_SDS220.qmd` | Full analysis (Quarto + R) |

## Reproduce

1. Download the FiveThirtyEight *Movies and the Bechdel Test* data ([fivethirtyeight/data/bechdel](https://github.com/fivethirtyeight/data/tree/master/bechdel)) and save it next to the `.qmd` as `Movies and the Bechdel Test - movies (3).csv`, or update the `read_csv()` path.
2. Render:

```r
install.packages(c("tidyverse", "infer", "kableExtra", "openintro", "broom"))
quarto::quarto_render("FINAL_PROJECT_SDS220.qmd")
```

## Data

Walt Hickey, ["The Dollar-And-Cents Case Against Hollywood's Exclusion of Women"](https://fivethirtyeight.com/features/the-dollar-and-cents-case-against-hollywoods-exclusion-of-women/), FiveThirtyEight (2014): about 1,800 films released 1970–2013 with Bechdel outcomes from BechdelTest.com and budgets and grosses from The-Numbers.com.
