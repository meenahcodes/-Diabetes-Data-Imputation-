
# Diabetes Data Analysis and Imputation Project

In this project, I cleaned and preprocessed the diabetes dataset, detected missing and anomalous values, and experimented with different imputation methods. 

## About the Dataset

I used the well-known Diabetes dataset, which contains medical data collected from 768 female patients in the Phoenix, Arizona area between 1965 and 1975. 
Each patient is described by 9 attributes:

 **Pregnancies:** Number of times the patient has been pregnant.
 **Glucose:** Plasma glucose concentration (mg/dl).
 **Blood Pressure:** Diastolic blood pressure (mm Hg).
 **Skin Thickness:** Triceps skinfold thickness (mm).
 **Insulin:** 2-Hour serum insulin (mu U/ml).
 **BMI:** Body mass index (kg/m²).
 **Diabetes Pedigree Function:** A score that indicates the likelihood of developing diabetes based on family history.
 **Age:** Age of the patient in years.
 **Outcome:** Whether the patient developed diabetes (1) or not (0).

# STEPS

# 1. Data Exploration

 **Loading the Data:**  
  I began by importing the dataset into a Pandas DataFrame so that I could easily explore and manipulate the data.

 **Descriptive Statistics and Visualization:**  
  -I used methods like `.describe()` to get summary statistics and plotted histograms and boxplots to understand the distribution of key attributes (e.g Glucose, BMI)
  - This helped me see the overall shape of the data and identify any unusual values or patterns.

# 2. Detecting Missing Values and Anomalies
**Missing Values:**  
  - I programmatically checked for missing values using `df.isnull().sum()`. 
  - I also noticed that for certain clinical measurements (like Glucose, Blood Pressure, etc.), a value of zero doesn't make sense.
  - So, I replaced zeros with `NaN` (Not a Number) to mark them as missing.

 **Anomaly Detection with IQR:**  
  - To detect outliers, I used the Interquartile Range (IQR) method. 
  - I calculated the 25th (Q1) and 75th (Q3) percentiles for each numeric column and defined outliers as values lying outside the range:
  
  This helped me flag data points that were significantly different from most of the data.

# 3. Handling Missing Values with Imputation

**Simple Imputation:**  
  I first experimented with median imputation, replacing missing values with the median for each column. Median is often preferred because it is robust to outliers.

**Regression Imputation:**  
  For a more informed imputation, I used a regression imputation technique:
  
  - I first ensured that all predictor variables (like Glucose, BMI, etc.) had no missing values (using median imputation as necessary).
  - Then, I built a linear regression model using complete cases (rows where the target variable, e.g., Insulin, wasn’t missing).
  - I used this model to predict and fill in the missing values for Insulin.

# 4. Evaluating the Imputation

**Visual Comparisons:**  
  I used visual tools like Kernel Density Estimate (KDE) plots and boxplots to compare the distributions of the original and imputed data.
  By overlaying these plots, I confirmed that the imputed values did not significantly distort the overall distribution. For example:
  
  - The KDE plots showed that the overall shape (peak, spread, and tails) of the Insulin distribution remained similar after imputation.
  - Boxplots helped me see that the central tendency and spread were preserved.

  **Comparing Methods:**  
  I also compared regression imputation against a simpler random imputation.
  The regression method produced a more informed distribution that aligned closely with the original data,
  whereas random imputation didn’t account for relationships among variables.



# Results 

**Quality of Imputation:**  
  The regression imputation maintained the natural distribution of the data, ensuring that the imputed values were in line with the original clinical measurements. 
  This is crucial for preserving the data's integrity, especially when used in later stages of analysis or predictive modeling.

**Handling Anomalies:**  
  By identifying and appropriately handling missing values and outliers, I was able to create a cleaner, more robust dataset for further analysis.


# How to Run This Project

1. **Clone the Repository:**  
   ```
   git clone https://github.com/yourusername/diabetes-data-imputation.git
   ```
   
2. **Install the Required Packages:**  
   Ensure you have Python 3.x installed. Then run:
   ```
   pip install -r requirements.txt
   ```
   
3. **Run the Jupyter Notebook:**  
   Open the Jupyter Notebook `diabetes_imputation.ipynb` to walk through the project step by step.
   
4. **Explore the Visuals:**  
   The notebook contains various plots comparing data distributions before and after imputation, so you can visually inspect how the methods impacted the data.
