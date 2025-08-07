# Predicting Customer Churn Timing and Lifetime Value in the Telecom Industry

This project tackles the business problem of customer churn in the telecom industry.  With increased demand for communication services during the COVID‑19 pandemic, retaining subscribers has become critical for telecom providers.  By building a machine learning model that predicts which customers are likely to leave, companies can proactively design retention strategies and focus marketing resources on the most at‑risk customers.

The repository contains a Jupyter notebook that performs the entire workflow—loading the data, exploratory data analysis, preprocessing, model training and evaluation—and a presentation/report that summarize the findings.  The key takeaways and recommended next steps are also presented.

## Project files

* **`Customer Churn Prediction Code.ipynb`** – Jupyter notebook with all the code used in the project.  It includes data loading, preprocessing, handling class imbalance with SMOTE, model training (logistic regression, random forest, and XGBoost), threshold optimization and evaluation, and SHAP‑based feature importance analysis.
* **`ML Customer Churn Project Report.pdf`** – Written report summarizing the problem statement, methodology, key results and business implications.
* **`Predicting Customer Churn Timing and Lifetime Value in the Telecom Industry (1).pptx`** – PowerPoint presentation that visually walks through the project overview, methodology, results, business impact, limitations, recommendations and next steps.
* **`README.md`** – This file.  It describes the project and provides instructions for running the code and publishing to GitHub.

## Data source

The data used in this project is the [Telco Customer Churn](https://www.kaggle.com/blastchar/telco-customer-churn) dataset from Kaggle.  It contains **7,043** customer records with demographics, account information, service usage, contract type and billing details.  The target variable is `Churn`, indicating whether the customer left the company in the last month.  Before SMOTE balancing, roughly **26 %** of the customers had churned.

> **Note:** The dataset is not stored in this repository because of size and distribution restrictions.  When running the notebook, ensure that the Telco Customer Churn dataset (`WA_Fn‑UseC_-Telco‑Customer‑Churn.csv`) is available in the same directory or modify the notebook to point to your data location.

## Methodology overview

1. **Exploratory Data Analysis (EDA):**  The notebook examines the distribution of each feature, checks for missing values, and visualizes relationships between customer attributes and churn.  Key observations include a high proportion of month‑to‑month contracts among churners and elevated churn rates among customers without technical support or online security services.

2. **Data preprocessing:**
   - Dropped non‑informative columns (e.g. `customerID`).
   - Filled missing numeric values with the median and categorical values with the mode.
   - Categorical variables were encoded using a combination of label encoding and one‑hot encoding.
   - Addressed class imbalance using **SMOTE** to synthetically oversample the minority class (churners), resulting in a balanced dataset.

3. **Model selection and training:**  Three models were evaluated:
   - **Logistic Regression** – baseline linear model.
   - **Random Forest** – ensemble of decision trees with strong recall and interpretability.
   - **XGBoost** – gradient‑boosted decision trees that often achieve state‑of‑the‑art performance.

   The decision thresholds were fine‑tuned using the precision–recall curve rather than relying on the default 0.5 probability cutoff.

4. **Evaluation:**  Models were assessed using **precision**, **recall**, **F1‑score** and **ROC‑AUC**.  Random Forest achieved the highest recall (≈93 %) and F1‑score (≈0.86) among the tested algorithms.  XGBoost offered a slightly better balance of precision and recall but a lower recall, while logistic regression had the most straightforward interpretation but lower overall performance.  Confusion matrices and precision–recall curves are included in the notebook and presentation.

5. **Feature importance & interpretability:**  A SHAP (SHapley Additive exPlanations) analysis was performed to explain feature contributions.  The top drivers of churn were:
   - **Contract type:** month‑to‑month contracts significantly increased churn risk.
   - **Online security & tech support:** lack of these services correlated with higher churn.
   - **Tenure:** customers with shorter tenure were more likely to churn.
   - **Monthly charges:** higher monthly fees increased churn risk.

   Business implications include focusing retention strategies on month‑to‑month customers, monitoring higher‑paying customers for dissatisfaction, and rewarding long‑tenured customers to encourage loyalty.

## How to run the notebook

1. Ensure you have Python 3.8+ installed with the following libraries:

   ```bash
   pandas numpy scikit‑learn imbalanced‑learn matplotlib seaborn shap xgboost jupyter
   ```

   If they are not installed, you can install them via `pip install -r requirements.txt` (create a `requirements.txt` with the above packages) or install individually.

2. Place the Telco Customer Churn dataset CSV file in the same directory as the notebook or edit the file path in the notebook’s data loading section.

3. Launch Jupyter Notebook:

   ```bash
   jupyter notebook
   ```

   and open **`Customer Churn Prediction Code.ipynb`**.  Execute the cells sequentially from top to bottom.  The notebook is documented with markdown cells explaining each step.

4. The notebook will print evaluation metrics and generate plots (feature importances, confusion matrices, precision–recall curves).  At the end, it shows SHAP plots to interpret the model.

## Results summary

* **Random Forest** delivered the highest recall (≈93 %) and F1‑score (≈0.86) for churn prediction.
* **XGBoost** yielded comparable accuracy but a slightly lower recall, making it less suitable for capturing churners.
* **Logistic Regression** provided balanced but lower recall and served as a baseline model.
* SMOTE oversampling significantly improved recall and F1‑score by balancing the dataset.
* SHAP analysis highlighted contract type, tech support/online security, tenure and monthly charges as the most influential features, guiding targeted retention strategies.

## Business impact and recommendations

Predictive modelling enables telecom operators to proactively retain high‑risk customers rather than relying on reactive measures.  By identifying churn drivers, the company can:

* **Targeted interventions:** adjust contract types, offer personalized promotions or add tech support packages to at‑risk customers.
* **Pricing strategy:** monitor customers with high monthly charges for dissatisfaction and tailor offers accordingly.
* **Loyalty incentives:** reward long‑tenured customers to strengthen loyalty.

The presentation and report outline further limitations (e.g., binary churn prediction only, potential shortcomings of SMOTE, unmodeled external factors) and propose next steps such as developing customer lifetime value (CLTV) models and enhancing the dataset with time‑based features.

## How to publish this project on GitHub

Follow these steps to upload the project files to your GitHub account for public viewing:

1. **Prepare your files:**  This repository includes the Jupyter notebook, report, presentation and `README.md`.  A compressed archive (`customer_churn_project.zip`) has been created for convenient upload.

2. **Sign in to GitHub:**  Visit [https://github.com/](https://github.com/) and log in with your GitHub credentials.

3. **Create a new repository:**
   - Click the “➕” icon in the upper right corner and choose **New repository**.
   - Give your repository a descriptive name (e.g. `customer‑churn‑prediction`) and optional description.
   - Set the repository to **Public** so others can view it.  Leave **Initialize this repository with a README** unchecked since you already have one.
   - Click **Create repository**.

4. **Upload the project files:**  On the newly created repository page, click **Upload files**, then either drag‑and‑drop the `customer_churn_project.zip` file or upload the individual files (`Customer Churn Prediction Code.ipynb`, `Predicting Customer Churn Timing and Lifetime Value in the Telecom Industry (1).pptx`, `ML Customer Churn Project Report.pdf` and `README.md`).  GitHub will automatically extract the folder structure if you upload individual files; if you upload the ZIP, ensure you click **Add file → Upload files → Choose your files** and then select the ZIP file.

5. **Unpack the ZIP (optional):**  If you uploaded the ZIP, GitHub will display it as a single binary file.  For better accessibility, you may prefer to extract the ZIP locally and upload the individual files instead.  Alternatively, after uploading the ZIP, click **Add file → Create new file**, copy the contents of this README into the new `README.md` file on GitHub, and commit.  This will ensure that visitors see the project description on the repository’s front page.

6. **Commit your changes:**  After uploading, scroll down to the commit message box, optionally enter a message such as “Initial commit”, and click **Commit changes**.

7. **Verify your repository:**  Navigate to the repository’s **Code** tab to ensure all files are present.  Click on the notebook and presentation to confirm that GitHub can render them.  You can also copy the repository URL and share it with others.

## License

Specify a license for your project if you intend others to reuse your work.  Common choices include MIT, Apache 2.0 and GPL.  You can add a `LICENSE` file in the repository or select a license when creating the repository.

## Acknowledgements

This project uses the [Telco Customer Churn](https://www.kaggle.com/blastchar/telco-customer-churn) dataset from Kaggle.  The modeling framework builds upon common machine learning techniques and uses the `scikit‑learn`, `imbalanced‑learn`, `SHAP` and `XGBoost` libraries.
