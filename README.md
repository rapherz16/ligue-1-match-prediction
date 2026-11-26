# Ligue 1 Match Prediction

A reconstructed academic machine learning project exploring three-class football match prediction: home win, draw and away win.

## Dataset

The supplied coursework archive contains eight CSV files, including 4,691 historical matches (August 2012–May 2025), 128,240 player appearances, 61,944 match events and 233 target fixtures (August 2025–March 2026). The original archive is not redistributed because its publication rights have not been verified.

## Methodology

- Audit and clean the eight input tables; join historical player appearances and match events at team-match level.
- Build 86 numerical features from past results, recent form, venue-specific statistics, Elo ratings, head-to-head records and historical player/event aggregates.
- Freeze features at the start of each season to avoid using target-season outcomes. Exclude current club metadata, actual lineups and other potentially unavailable information.
- Compare a majority baseline, logistic regression, random forest and histogram gradient boosting using expanding-season validation (2020–2023).
- Select by mean macro F1 and evaluate once on the reserved 2024–25 season.

## Results

Mean validation metrics (equal weight per season):

| Model | Accuracy | Balanced accuracy | Macro F1 |
|---|---:|---:|---:|
| Logistic regression | 0.448 | 0.413 | 0.390 |
| Gradient boosting | 0.439 | 0.401 | 0.384 |
| Random forest | 0.471 | 0.411 | 0.351 |
| Majority baseline | 0.405 | 0.333 | 0.192 |

Logistic regression was selected. On the 306-match 2024–25 holdout it achieved **50.33% accuracy**, **43.35% balanced accuracy** and **0.417 macro F1**, versus **46.73% accuracy** and **0.212 macro F1** for the majority baseline. The model generated 233 retrospective predictions for the target file; target labels are not supplied, so no target-season score is claimed.

## Reproduce

1. Obtain the original `Foot.zip` coursework dataset and place it in the repository root (or its parent directory).
2. Install dependencies: `pip install -r requirements.txt`.
3. Open and run `ligue1_prediction.ipynb` in Jupyter. Outputs and plots are already included in the executed notebook.

## Limitations

Fixed pre-season information cannot capture within-season injuries, transfers or current form. Promoted clubs may have sparse historical data. Player valuation and lineup tables were audited but not used as model features in this version. The project is a retrospective educational experiment, not a live prediction service.

## Repository files

- `ligue1_prediction.ipynb`: executed analysis and model comparison.
- `results/`: validation scores, holdout scores and target predictions.
- `requirements.txt`: dependencies.
