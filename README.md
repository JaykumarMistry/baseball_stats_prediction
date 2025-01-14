# Baseball Stats Prediction with Machine Learning

## Project Overview

This project leverages machine learning techniques to predict the **next season's WAR (Wins Above Replacement)** for Major League Baseball players based on their historical performance. Using data from the `pybaseball` library and advanced regression techniques, the model aims to provide accurate predictions and identify key performance indicators for players.

---

## Dataset

### Source
- Data was sourced using the `pybaseball` library for the years **2002 to 2022**.
- Additional documentation: [FanGraphs Player Stats](https://www.fangraphs.com/).

### Preprocessing Steps
1. Data fetched and stored locally (`batting.csv`).
2. Filtered players with multiple seasons of data.
3. Created a new target variable: `Next_WAR` (WAR of the following season).
4. Cleaned dataset by:
   - Removing columns with missing values.
   - Dropping redundant or non-numerical columns (e.g., team names).
5. Scaled numerical features using `MinMaxScaler`.

---

## Machine Learning Pipeline

### Feature Selection
- Used `SequentialFeatureSelector` with Ridge Regression to select top 20 features.
- Final predictors:
  ```
  ['Age', 'IBB', 'SO', 'SB', 'BU', 'BABIP', 'IFH%', 'WAR', 'Spd', 'PH', 
   'CB%', 'Z-Contact%', 'SwStr%', 'wGDP', 'Oppo%', 'SLG+', 'LD+%', 'Pull%+', 
   'Soft%+', 'Hard%+']
  ```

### Additional Features
- Player-specific metrics:
  - `player_season`: Number of seasons a player has played.
  - `war_corr`: Correlation of `WAR` with player experience.
  - `war_diff`: Year-over-year difference in `WAR`.
- League-wide metrics:
  - `war_season`: Normalized `WAR` by season.

### Model
- **Model**: Ridge Regression (`alpha=1`)
- **Backtesting**: Evaluated predictions year-by-year to simulate real-world forecasting.
- **Performance Metric**: Mean Squared Error (MSE)

### Results
- Baseline MSE: `2.77`
- After adding new features: `2.67`

---

## Key Insights
1. **Top Positive Features**:
   - `war_season`: Indicates league-wide normalization trends.
   - `Hard%+`: Percentage of hard-hit balls.
2. **Top Negative Features**:
   - `Age`: Negative impact of aging on player performance.
   - `WAR`: Suggests potential regression for players with standout seasons.
3. **Challenges**:
   - Outliers (e.g., Bryce Harper 2014, Buster Posey 2010) significantly impacted accuracy.
   - Linear model struggled to capture non-linear dynamics.

---

## Repository Structure
```plaintext
📁 baseball-stats-prediction
├── 📄 batting.csv              # Preprocessed dataset
├── 📄 main.ipynb               # Main Jupyter notebook script for the project
├── 📄 requirements.txt         # Dependencies for the project
├── 📄 README.md                # Project documentation (this file)
```

---

## Setup Instructions

1. **Clone the Repository**
   ```bash
   git clone https://github.com/JaykumarMistry/baseball_stats_prediction.git
   cd baseball_stats_prediction
   ```

2. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

---

## Future Improvements

1. Incorporate non-linear models (e.g., Random Forest, XGBoost) to capture complex player dynamics.
2. Perform hyperparameter tuning for Ridge Regression and alternative models.
3. Visualize predictions and actual values for better insights.

---

## License
This project is licensed under the MIT License. See the LICENSE file for details.

---

## Acknowledgments
- [PyBaseball](https://github.com/jldbc/pybaseball): Baseball data retrieval library.
- [FanGraphs](https://www.fangraphs.com/): Source for player statistics.
- I would like to thank @Dataquestio, whose YouTube tutorials on machine learning were really helpful to building this project.