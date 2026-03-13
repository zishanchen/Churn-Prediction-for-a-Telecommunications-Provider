# Churn Prediction for a Telecommunications Provider

> **Predicting customer churn for a telecommunications provider using machine learning and business analytics.**

## Project Overview
As a data analyst for a telecommunications company facing a high churn rate, the goal of this project is to build a predictive model to identify which customers are most likely to cancel their subscriptions next. By accurately flagging at-risk customers, the business can proactively implement targeted retention strategies.

## Dataset
The analysis is based on a relational database format split across four core datasets, located in the `data/raw/` directory:

* **`customers.csv`**: Contains demographic information (e.g., gender, age, dependents, partner status) and internet type.
* **`service_options.csv`**: Details the services each customer has signed up for (e.g., internet, phone, multiple lines, unlimited data, referrals).
* **`payment_info.csv`**: Includes account and billing information (e.g., contract type, payment method, monthly charges, total revenue).
* **`churn_analysis.csv`**: Contains the target variable (`churn`) indicating whether the customer left or stayed.

## Repository Structure
```
├── data/                   # Directory for all data files
│   ├── raw/                # Original, immutable data
│   │   ├── churn_analysis.csv
│   │   ├── customers.csv
│   │   ├── payment_info.csv
│   │   └── service_options.csv
│   └── outputs/            # Generated files and predictions
│       ├── predictions.csv
│       └── sample_prediction.csv
│
├── notebooks/              # Jupyter notebooks
│   └── Churn_Prediction.ipynb
│
├── README.md               # The top-level README for developers
├── requirements.txt        # The dependencies for reproducing the environment
```
## Methodology
1. **Data Wrangling:** Merged the customer profile, payment information, and churn datasets into a single unified dataframe. Handled missing values in demographic and service columns by imputing the most frequent values (mode).
2. **Data Preprocessing:** Standardized financial units by converting cents to dollars. Applied one-hot encoding to all categorical and string variables to prepare them for mathematical modeling. 
3. **Feature Selection:** Dropped statistically insignificant variables to refine the model, isolating key drivers such as age, dependents, technical support, contracts, and payment methods.
4. **Predictive Modeling:** Trained a Logistic Regression model using `statsmodels` (`smf.logit`) to calculate the probability of a customer churning. 
5. **Evaluation:** Converted predicted probabilities into binary outcomes (using a 0.5 threshold) and evaluated the model using the **Balanced Accuracy Score** to account for potential class imbalances.

## Results & Output
The optimized logistic regression model successfully identifies customers at risk of churning, achieving a balanced accuracy score of approximately **0.75** across the evaluated sets. 

The model was then applied to the unlabelled dataset (customers without a documented churn status). These final predictions have been exported to **`predictions.csv`**, formatted with two columns (`customer_id` and `prediction`) matching the requested submission structure.

## How to Run the Project
1. **Clone the repository:**
   ```
   git clone https://github.com/zishanchen/churn-prediction-for-a-telecommunications.git
   ```
2. **Create a virtual environment and install dependencies:**
   ```
   python -m venv venv
   # On macOS/Linux:
   source venv/bin/activate  
   # On Windows:
   venv\Scripts\activate
   
   pip install -r requirements.txt
   ```
3. **Launch Jupyter Notebook:**
   ```bash
   jupyter notebook
   ```
Navigate to the notebooks`/ directory`, open `Churn_Prediction.ipynb`, and run the cells sequentially to reproduce the data cleaning, model training, and prediction generation.
## License
This project is open-source and available under the [MIT License](LICENSE).
