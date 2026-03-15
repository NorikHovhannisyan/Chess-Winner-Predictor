# ♟️ Chess Match Winner Predictor
## This project aims to predict the outcome of chess matches played on Lichess using Machine Learning. The journey involves data preprocessing, feature engineering, and a deep dive into avoiding Data Leakage to build a reliable real-time predictor.

## 🚀 Project Overview
The goal is to determine whether White or Black will win (or if the game will end in a draw) based on pre-game information such as player ratings and opening choices.

## Key Technical Achievements:
- Data Cleaning & Engineering: Transformed raw chess metadata into model-ready numerical features.
- Leakage Detection: Identified and removed "future" features that artificially inflated model accuracy.
- Model Optimization: Utilized XGBoost for high-performance classification.
- Validation: Performed 5-fold Cross-Validation to ensure the model's stability and reliability.

## 🔍 The "Data Leakage" Insight
### One of the most critical parts of this project was the transition from a "perfect" model to a "realistic" one.
- Initial Approach: Using features like turns and victory_status, the model achieved an impressive ~89% accuracy.
- The Discovery: Feature importance analysis revealed that the model was heavily relying on status_draw and turns. In a real-world scenario, these are unknown before the game ends.
- The Solution: I removed all post-game features to build a Real-Time Predictor.

## 📊 Final Results
### After refining the feature set, the model's performance reflects true predictive power:
- Real-time Accuracy: ~62.3%.
- Key Feature: rating_diff (the difference between White and Black ratings) became the primary predictor.
- Stability: A standard deviation of only 0.49% across cross-validation folds.

## 🛠️ Installation & Usage
### Requirements
``` Ensure you have the following libraries installed:
pip install pandas xgboost scikit-learn matplotlib
```
### Quick Prediction
```You can use the saved model (chess_predictor.pkl) to make predictions:

Python
import pickle
import pandas as pd

# Load the trained model 
with open('chess_predictor.pkl', 'rb') as f:
    model = pickle.load(f)

# Example: Predicting a match outcome
# Input data must match the training feature structure
prediction = model.predict(new_data)
print(f"Predicted Winner: {prediction}")
```
## 📂 Repository Structure
- Game Chess.ipynb: Full analysis and model training workflow.
- chess_predictor.pkl: The final trained XGBoost model.
- games.csv: The dataset used for training and testing.
- Requirements.txt: List of dependencies.
