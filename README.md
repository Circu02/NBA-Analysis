# NBA Performance Analysis: Comparing 10 All-Time Greats (1985–2025)

A data analysis project that builds a 56,000+ record NBA dataset and uses Python and SQL to compare 10 all-time great players: Michael Jordan, LeBron James, Tim Duncan, Kobe Bryant, Shaquille O'Neal, Hakeem Olajuwon, Stephen Curry, Kevin Durant, Nikola Jokic, and Giannis Antetokounmpo.

## Questions explored
- **Playoff efficiency:** Which players' true shooting % (TS%) rises or falls from the regular season to the playoffs?
- **Finals difficulty:** How hard were each player's Finals, based on pre-series betting odds?
- **Aging curves:** How did each player's impact (BPM) change with age? K-Means clustering splits careers into early, prime, and late phases.
- **Award accuracy:** Did MVP, DPOY, and Finals MVP voting reward the statistically best player?
- **Career phase prediction:** Can a KNN model identify a player's career phase from his stats alone?
- **Positional dominance:** How far above other players at their position, in the same season, was each player? (z-scores)

## Data
| Dataset | Source | Method |
|---|---|---|
| Per-game box scores, 1985–2025 (regular season + playoffs) | Basketball-Reference | Downloaded tables |
| Advanced stats (PER, TS%, BPM, WS, VORP) | Basketball-Reference | Downloaded tables |
| Awards and All-NBA/All-Defensive teams | Basketball-Reference | Web scraping (BeautifulSoup) |
| Single-game career highs | NBA API (`nba_api`) | API |
| Finals betting odds | Covers.com | Web scraping |

## Tools
Python (pandas, NumPy, scikit-learn, Matplotlib, BeautifulSoup, requests), SQL (SQLite), Jupyter

## SQL analysis
The notebook's **SQL Analysis** section loads all five cleaned datasets into a SQLite database (`nba.db`) and answers several questions directly in SQL:
1. Regular-season vs. playoff TS% (minutes-weighted, conditional aggregation)
2. League 3-point attempt rate, scoring, and TS% by decade (subquery join)
3. Each player's peak season by BPM (`ROW_NUMBER()` window function)
4. Award totals by player (MVP, DPOY, Finals MVP, All-NBA, All-Defensive)
5. Most efficient 25+ PPG seasons since 1985 (join of per-game and advanced stats)
6. Biggest Finals upsets by betting odds

## Machine learning
- **K-Means clustering** splits each player's career into Early Career, Prime Years, and Late Career phases.
- **K-Nearest Neighbors (KNN)** predicts a season's career phase from performance stats alone, without age. It uses feature scaling, chooses *k* by 5-fold cross-validation, evaluates on a held-out test set against a baseline, and shows a confusion matrix.
- **Linear regression** rates each season's award candidates from their stats, and those ratings are compared with the actual MVP, DPOY, and Finals MVP winners.

## How to run
```bash
pip install pandas numpy scikit-learn matplotlib beautifulsoup4 requests ftfy nba_api
```
Open `NBA Performance Analysis Project.ipynb` and run all cells from top to bottom. The data collection cells create the CSV files that the analysis, KNN, and SQL sections use.
