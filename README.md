# Insurance-Prediction
This Django-based web application allows users to predict medical insurance charges using a machine learning model (RandomForestRegressor). Users can input personal data (age, sex, BMI, number of children, smoking status, and region), and the app will return a predicted insurance cost : https://drive.google.com/file/d/11gCjdlouuSjL25MhxgxCYdIaW6MVYIxa/view?usp=sharing

## Technologies Used : 
- Backend Framework: Django
- Machine Learning: Python with library : scikit-learn, joblib
- Frontend: HTML, (Templates : Bootstrap and tailwindcss)

## Features : 
- Base.html : Shared layout with header/footer
- index.html : Home page with app introduction, benefits, and use case
- about.html : Personal bio / About Jessie Angelica
- prediction.html : Page with form to enter inputs and show prediction result
- contact.html : Contact form or contact details page

## Django Steps
1. Create Django App : python manage.py startapp home
2. Apply Migrations : python manage.py migrate
3. Create Superuser : python manage.py createsuperuser
4. Set Up Virtual Environment : venv\Scripts\activate
5. Install Required Packages : pip install django joblib scikit-learn
6. Run the Development Server : python manage.py runserver
7. Access the Application : http://127.0.0.1:8000/

## URL Routing
- /insurance/home/urls.py : This file defines URL patterns for the home app. It maps URL paths (like /about/, /prediction/) to specific view functions (like views.about, views.prediction) that handle the corresponding HTTP requests.
- /insurance/insurance/urls.py : This is the main project-level URL router. It includes delegates all other URL paths to your home app using include('home.urls') and Directs specific paths (like /admin/) or groups of paths (like '/') to appropriate app routers.
- /insurance/home/views.py : A view receives HTTP requests, processes data (e.g. predicting with a model), and returns HTML responses rendered with templates.
  - home() – Renders the home page.
  - about() – Renders the about page.
  - contact() – Renders the contact page.
  - prediction() – Handles form submission, uses a ML model to make predictions, and renders the result on the page.

## Flow
- User navigates to /prediction/
- Fills in the form (age, sex, bmi, etc.)
- Submits form → POST request to prediction() view
- Model predicts charge → result shown on prediction.html

## Prediction Model
The model is a RandomForestRegressor stored in the /static folder as random_forest_regressor. It is trained to predict insurance charges based on:
- Age
- Sex (0 = female, 1 = male)
- BMI
- Number of children
- Smoker (0 = no, 1 = yes)
- Region (encoded as integer)


## Python Code
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

