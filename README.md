# Socio-Spatial Analysis of Housing Prices in Paris

## Overview

This project explores housing price variation in Paris using the French DVF (Demande de Valeurs Foncières) dataset. The objective is to analyze how structural, spatial, and temporal factors influence property prices, and to evaluate the effectiveness of a baseline machine learning model in capturing these dynamics.

The study focuses on predicting the price per square meter (€/m²) for apartment transactions in Paris.

## Data

- Source: French DVF dataset (open government data)
- Scope: Real estate transactions in Paris
- Filtering criteria:
  - Apartments only (`type_local = Appartement`)
  - Sales only (`nature_mutation = Vente`)
  - Single-lot transactions (`nombre_lots = 1`)
  - Removal of missing values and outliers

## Data Preparation

Key preprocessing steps include:

- Cleaning and filtering raw transaction data  
- Removing duplicate transactions (`id_mutation`)  
- Constructing price per square meter:

```python
prix_m2 = valeur_fonciere / surface_reelle_bati

	•	Applying log transformation:

log_prix_m2 = np.log(prix_m2)

	•	Extracting temporal features:
	•	Year
	•	Month
	•	Constructing spatial feature:
	•	Arrondissement (derived from postal code)

⸻

## Features

Numerical Features
	•	Surface area (surface_reelle_bati)
	•	Number of rooms (nombre_pieces_principales)
	•	Year of transaction

Categorical Features
	•	Arrondissement
	•	Month

⸻

Modeling

A baseline linear regression model is implemented using a preprocessing pipeline:
	•	One-hot encoding for categorical variables
	•	Direct use of numerical features
	•	Model: LinearRegression (scikit-learn)

from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.linear_model import LinearRegression


⸻

Evaluation

Model performance is evaluated using:
	•	R² (coefficient of determination)
	•	RMSE (in log space)
	•	MAE (€/m², after inverse transformation)

⸻

Results

The baseline model achieves low explanatory power (R² close to 0), indicating that the selected features are insufficient to fully capture housing price variation in Paris.

However, the model provides a useful benchmark and highlights key challenges in real estate price modeling.

⸻

Discussion

Several factors explain the limited performance:
	•	Missing property-level features (e.g., building age, condition, amenities)
	•	Coarse spatial granularity (arrondissement-level)
	•	Nonlinear relationships between features and price

⸻

Conclusion

This project demonstrates both the potential and limitations of using administrative transaction data for housing price modeling.

Future improvements may include:
	•	Incorporating fine-grained spatial features (e.g., coordinates)
	•	Using richer datasets with more property attributes
	•	Applying nonlinear models (e.g., tree-based methods)

⸻

Tech Stack
	•	Python
	•	Pandas / NumPy
	•	scikit-learn
	•	Jupyter Notebook

