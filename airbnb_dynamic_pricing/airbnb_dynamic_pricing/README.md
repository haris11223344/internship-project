# Airbnb Dynamic Pricing Recommendation Engine

Turnkey project: synthetic data, scikit-learn model, CLI tools, Tableau-ready CSV, and Excel template.

## Quick Start

```bash
# 1) (Optional) Create a virtual env and install deps
pip install -r requirements.txt

# 2) Train (already trained model is included)
python src/train_model.py --csv data/airbnb_listings_synthetic.csv --out models/pricing_model.joblib

# 3) Single prediction (CLI)
python src/recommend_price.py   --model models/pricing_model.joblib   --city "Mumbai" --neighbourhood "Bandra" --property_type "Entire home/apt"   --accommodates 4 --bedrooms 2 --bathrooms 2 --beds 2   --review_score 4.7 --reviews_count 35 --superhost 1 --amenity_count 14   --cleaning_fee 10 --month 12

# 4) Tableau
# Open tableau/airbnb_pricing_for_tableau.csv and follow tableau/dashboard_guide.txt
```

## What’s Inside

- `data/airbnb_listings_synthetic.csv` — 8k rows synthetic listings with seasonality & location effects.
- `models/pricing_model.joblib` — RandomForest pipeline with OneHot + Scaling (already trained).
- `src/train_model.py` — Train a new model.
- `src/recommend_price.py` — CLI to get a price suggestion + bounds.
- `notebooks/01_explore_and_model.ipynb` — E2E notebook (explore, train, export Tableau CSV).
- `tableau/airbnb_pricing_for_tableau.csv` — Subsampled dataset with suggested_price, price_delta, quality_index.
- `tableau/dashboard_guide.txt` — Step-by-step dashboard guide including a price target slider.
- `excel/Price_Recommendation_Template.xlsx` — Input template (CSV fallback provided if Excel lib not available).
- `outputs/recommendations.csv` — Sample batch of suggested prices for 250 listings.
- `outputs/feature_importances.csv` — Model feature importances.

## Metrics

{
  "note": "Model trained on 2,500-row sample for speed",
  "r2": 0.8576697818552547,
  "mae": 10.031750705084615
}

## Requirements

- Python 3.9+
- Packages:
  - scikit-learn
  - joblib
  - pandas
  - numpy
  - (optional) openpyxl for Excel template

Install:
```bash
pip install -r requirements.txt
```

## Notes

- Data is synthetic and safe to share.
- Use the CLI or the notebook to generate new recommendations.
- For production, consider gradient boosting (XGBoost/LightGBM), cross-validation, holiday effects, minimum-stay pricing, and demand-side features (search volume, occupancy).
