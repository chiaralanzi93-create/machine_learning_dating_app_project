# Can We Predict Mutual Matches on a Dating App?

## 🛠️ Tech Stack & Tools

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![pandas](https://img.shields.io/badge/pandas-Data%20Analysis-purple?logo=pandas)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-lightgrey?logo=numpy)
![scikit-learn](https://img.shields.io/badge/scikit--learn-Machine%20Learning-orange?logo=scikit-learn)
![imbalanced-learn](https://img.shields.io/badge/imbalanced--learn-SMOTE-red)

![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-blue)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-lightblue)

![uv](https://img.shields.io/badge/uv-Python%20Environment-green)
![Git](https://img.shields.io/badge/Git-Version%20Control-black?logo=git)
![GitHub](https://img.shields.io/badge/GitHub-Repository-black?logo=github)

---

## Presentation

📊 **Project Slides (Canva)**  
View the full presentation here:  
👉 https://www.canva.com/design/DAG-bS4Xx9Q/Ezfifk2RZBerM0oKQ0Lvew/edit?utm_content=DAG-bS4Xx9Q&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton

---

## Project Overview

This project explores whether **mutual matches on a dating app can be predicted** using supervised machine learning techniques.

The task is framed as a **binary classification problem**, aiming to estimate the likelihood that two users will form a mutual match.

Accurate match prediction can:
- Improve **user experience** by reducing ineffective interactions  
- Enhance **platform efficiency** by prioritizing high-quality recommendations  

---

## Dataset

- **Source**: Kaggle – Dating App Behavior Dataset  
- **Content**:
  - User attributes (demographics & profile information)
  - Behavioral characteristics (app usage, swipe behavior, messaging activity)
  - Match outcomes

### Target Variable

The original target variable `match_outcome` contains multiple categories (e.g. date happened, ghosted, blocked).

For this project, outcomes were grouped into:
- **Positive (1)**: mutual match  
- **Negative (0)**: all other outcomes  

The positive class represents approximately **40%** of the data, making this an **imbalanced classification problem**.

---

## Data Cleaning & Preparation

The dataset is clean and well-structured:
- No missing or null values  
- No duplicate records  
- Key numerical variables fall within realistic ranges  
- Distribution checks (boxplots) show no significant outliers  

No heavy data cleaning was required before modeling.

---

## Feature Engineering

Different preprocessing techniques were applied based on feature type:

- **Numerical features**: StandardScaler  
- **Ordinal features**: Label Encoding  
- **Nominal features**: One-Hot Encoding  

### Interest Tags Processing

The `interest_tags` feature required special handling:
- Users can have up to three interests, resulting in over 40,000 unique combinations
- Direct one-hot encoding would create extremely sparse features

Steps applied:
1. Split and explode interest tags  
2. Reduce to 49 unique interests  
3. Group interests into three categories:
   - Social-based  
   - Solo-oriented  
   - Mixed  

This preserves meaningful information while keeping the feature space manageable.

---

## Feature Selection

Feature relevance was assessed using diagnostic methods:

- **Numerical features**: Variance Inflation Factor (VIF < 5), indicating low multicollinearity  
- **Categorical features**: All p-values > 0.05, indicating no strong standalone association  

This suggests that mutual matches are driven by **multiple features jointly**, rather than any single dominant factor.

---

## Model Building

Three supervised learning models were tested:

### Logistic Regression
- Simple and interpretable baseline model  
- Performance close to random guessing  
- SMOTE did not significantly improve results  

### Decision Tree
- Captures non-linear relationships  
- High recall for the positive class  
- Lower precision and risk of overfitting  

### Random Forest (Final Model)
- Hyperparameters tuned using RandomizedSearchCV  
- More stable generalization  
- Better balance between precision and recall  

---

## Model Evaluation

Evaluation metrics:
- Accuracy  
- Precision (Class 1)  
- Recall (Class 1)  
- F1-score (Class 1)  

| Model                | Accuracy | Recall (1) | F1 (1) | Strength |
|---------------------|----------|------------|--------|----------|
| Logistic Regression | ~0.50    | ~0.48      | ~0.44  | Simple & interpretable |
| Decision Tree       | ~0.46    | ~0.72      | ~0.51  | High recall |
| Random Forest       | ~0.53    | ~0.35      | ~0.37  | Best overall balance |

The **Random Forest** model was selected as the final model due to its robustness and generalization ability.

---

## Key Findings

1. **Limited Predictability**  
   Mutual match behavior shows high randomness and moderate predictability.

2. **Behavior > Demographics**  
   Behavioral features (usage time, likes received, message activity) are more informative than demographics.

3. **Precision–Recall Trade-off**  
   Clear trade-offs indicate a **high-noise, weak-signal** prediction problem.

---

## Real-World Application

The model can be used to:
- Estimate the probability of a mutual match  
- Prioritize recommendations with higher predicted success  
- Reduce wasted interactions and improve user experience  

---

## Challenges & Limitations

- Limited feature set (no profile photos or message content)  
- Strong behavioral overlap between matched and unmatched users  
- Class imbalance and noisy labels  

---

## Future Work

- Incorporate text and image embeddings  
- Experiment with gradient boosting models  
- Apply ranking-based recommendation approaches  
- Include temporal or sequential interaction data  

---

## Conclusion

**Can we predict mutual matches on a dating app?**  
Yes — **to a certain extent**.

Machine learning can extract useful signals from user behavior, but human decision-making is complex and cannot be fully captured by the available data.

---

## Authors

- Ou  
- Chiara  
- Veerpal  

Date: 16.01.2026
