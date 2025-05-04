# Insurance-Prediction
Insurance-Prediction using Django and Python :
https://drive.google.com/file/d/11gCjdlouuSjL25MhxgxCYdIaW6MVYIxa/view?usp=sharing

**1. Importing Libraries**

**2. Loading and Inspecting the Data**

Loads the insurance dataset into a DataFrame from a local CSV file.
- .info(): Overview of dataset – data types, non-null counts.
- .describe(): Summary statistics for numerical features.
- .describe(include='all'): Includes all columns, even categorical ones.
- .isnull().sum(): Checks for missing values.
- .shape: Returns the number of rows and columns in the DataFrame. (1338, 7) indicates 1338 rows and 7 columns.
- Removes any duplicate rows from the dataset.

**3. Visualizing Distributions and Outliers**
- Iterates through selected numeric columns to:
- Plot histograms (left) using sns.distplot to visualize distributions.
- Plot boxplots (right) using sns.boxplot to detect outliers and see spread of values.

**4. Encoding Categorical Variables**

Converts categorical variables into numerical formats for machine learning models:
- sex: female → 0, male → 1
- smoker: no → 0, yes → 1
- region: Mapped to integer values for simplicity (could also use one-hot encoding in other scenarios).

**5. Feature and Target Separation**
- x: Feature matrix (independent variables).
- y: Target variable (dependent variable, i.e., insurance expenses).

**6. Splitting Data into Training and Testing Sets**
- Splits data into training (80%) and testing (20%) sets.
- random_state=42 ensures reproducibility.

**7. Model Training and Evaluation**
- Trains a Linear Regression model : Model performance. 0.8068 indicates good fit.
- Trains a Support Vector Regressor : Performs poorly here (score2 = -0.134), likely due to data scaling issues (SVR is sensitive to feature scaling).
- Trains a Random Forest ensemble model : Performs well with structured tabular data (better than linear/SVR in many cases).

**8. Making Predictions with New Data**
- Prepares a new input (e.g., a 19-year-old female smoker).
- Predicts medical expenses using the trained Random Forest model.

**9. Saving the Model**

Saves the trained Random Forest model using joblib for future reuse without retraining.

