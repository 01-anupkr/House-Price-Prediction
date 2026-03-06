<p align="center">
  <img src="assets/banner.png" alt="House Price Prediction Banner" />
</p>
# 🏠 House Price Prediction

**Project Type:** Data Preprocessing & Regression Modeling  
**Source:** [Kaggle - House Prices: Advanced Regression Techniques](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/anupkumar/House-Price-Prediction/blob/main/house_price_preprocessing.ipynb)

---

## 🎯 Objective

Prepare the Ames Housing dataset for regression modeling by applying:
- ✅ Data cleaning & missing value imputation  
- ✅ Label Encoding for categorical features  
- ✅ Log transformation of the target variable (`SalePrice`)  
- ✅ Train/test splitting and evaluation using RMSE  

---

## 📁 Project Structure
```
House-Price-Prediction/
├── assets/
│   └── banner.png
├── data/
│   ├── train.csv
│   ├── test.csv
│   ├── sample_submission.csv
│   └── data_description.txt
├── house_price_preprocessing.ipynb  # Main notebook
├── submission.csv                   # Generated output (after model run)
├── requirements.txt                # Python dependencies
├── .gitignore                      # Files to exclude from Git tracking
├── LICENSE                         # MIT License
└── README.md                       # Project documentation

```



---

## ⚙️ Features Processed

- 🔍 Imputed missing values (median for numerics, "Missing" for categoricals)
- 🔁 Combined train & test before encoding to handle unseen labels
- 🔢 Applied `LabelEncoder` for all categorical features
- 🔄 Performed `log1p()` transformation on `SalePrice`
- 🧪 Split data into training and validation sets

---

## 📊 Libraries Used

- `pandas` — Data manipulation  
- `numpy` — Numerical operations  
- `matplotlib` & `seaborn` — Visualizations  
- `scikit-learn` — Preprocessing, modeling, evaluation  

---

## 🔧 How It Works (Step-by-Step)

The entire pipeline runs inside `house_price_preprocessing.ipynb` and follows these steps:

### 1. Data Loading
- Loads `train.csv` (1460 rows, 81 features including `SalePrice`) and `test.csv` (1459 rows, 80 features) from the `data/` folder using `pandas.read_csv()`.

### 2. Dropping High-Missing Columns
- Any column with more than **40%** missing values is dropped from both train and test sets. This removes noisy features like `Alley`, `PoolQC`, `Fence`, `MiscFeature`, and `FireplaceQu`.

### 3. Missing Value Imputation
- **Numeric columns** → filled with the **median** of that column.
- **Categorical columns** → filled with the string `"Missing"`.
- This is done for both train and test sets to ensure no `NaN` values remain.

### 4. Label Encoding Categorical Features
- All categorical (object-type) columns are encoded to integers using `sklearn.preprocessing.LabelEncoder`.
- Train and test data are **combined before fitting** the encoder so that all possible category labels are seen — this prevents errors from unseen labels in the test set.

### 5. Log Transformation of Target Variable
- `SalePrice` is transformed using `np.log1p()` (log(1 + x)) to reduce right-skew and make the distribution more normal, which improves Linear Regression performance.

### 6. Train/Validation Split
- The training data is split **80/20** using `train_test_split(random_state=42)` to create a validation set for evaluating model performance.

### 7. Model Training (Linear Regression)
- A `LinearRegression` model from scikit-learn is trained on the 80% training split.
- The model learns coefficients for each feature to predict `log(SalePrice)`.

### 8. Evaluation (RMSE)
- Predictions are made on the 20% validation set.
- **Root Mean Squared Error (RMSE)** is computed between predicted and actual `log(SalePrice)` values.
- The RMSE is printed to the console as the primary evaluation metric.

### 9. Test Set Prediction & Submission
- The trained model predicts `log(SalePrice)` for the test set.
- Predictions are **reverse-transformed** using `np.expm1()` to convert back to actual dollar values.
- Results are saved to `submission.csv` with columns `Id` and `SalePrice`.

### 10. Visualizations
- **SalePrice Distribution**: Side-by-side histogram comparing original vs. log-transformed `SalePrice`.
- **Correlation Heatmap**: Top 10 features most correlated with `SalePrice` displayed as an annotated heatmap.
- **Scatter Plots**: Top 3 correlated features plotted against `SalePrice` to visualize linear relationships.

---

## 🚀 How to Run the Project

1. ✅ **Install Required Libraries**
   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn
   ```

2. 📂 **Download and Unzip the Project Folder**

   Make sure the folder structure looks like this:
   ```
   house-price-prediction/
   ├── house_price_preprocessing.ipynb
   └── data/
       ├── train.csv
       └── test.csv
   ```

3. 🧠 **Run the Notebook**

   - Open `house_price_preprocessing.ipynb` in **Jupyter Notebook** or **VS Code**
   - Run all cells sequentially to execute data preprocessing, model training, and evaluation

4. 📄 **Generate Predictions**

   After running all cells, a file named `submission.csv` will be generated:
   submission.csv

---

## 📎 Dataset Credit

📊 Data provided by Kaggle:House Prices - Advanced Regression Techniques(https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data)

---

## 🙋‍♂️ Author

**Anup Kumar**  
💻 [GitHub](https://github.com/anupkumar)  

---

# House-Price-Prediction
🏠 Predict house prices using Linear Regression and data preprocessing (Kaggle dataset). Includes data cleaning, label encoding, feature engineering, and model evaluation.
