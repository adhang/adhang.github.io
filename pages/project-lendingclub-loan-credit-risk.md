# LendingClub - Loan Credit Risk Prediction

This is my internship project as a data scientist at [id/x partners](https://idxpartners.com/)
<br><br>

In this project, I designed a predictive model to determine the probability that loan borrowers will have a good or bad (risky) loan status at a lending company and achieve an **accuracy score of 98%**.
<br><br>

Note: This project is still on-going, will update later.

## Project Notebooks

[![Readme Card](https://github-readme-stats.vercel.app/api/pin/?username=adhang&repo=
lendingclub-loan-credit-risk&show_owner=true&title_color=00875A&icon_color=006644&text_color=1B262C&bg_color=F5F7FA)](https://github.com/adhang/lendingclub-loan-credit-risk)

I create separated notebooks due to my limited computing resources
- [Exploratory Data Analysis](https://github.com/adhang/lendingclub-loan-credit-risk/blob/main/LendingClub_Loan_Credit_Risk_EDA.ipynb)
- [Machine Learning Modeling](https://github.com/adhang/lendingclub-loan-credit-risk/blob/main/LendingClub_Loan_Credit_Risk_Modeling.ipynb)

## Dataset & Business Understanding

**Dataset Information**
- This dataset contains borrowers information from a lending company, named [LendingClub](https://www.lendingclub.com/) (LC for short) from 2007 to 2014
- This company has various offerings such as borrowing, banking, and investing
<br><br>

**Attribute Information**
- Identifier
	- `id` - A unique LC assigned ID for the loan listing
	- `member_id` - A unique LC assigned ID for the borrower member

- Target Variable
	- `loan_status` - Current status of the loan, whether it's a good or bad (risky)

- More detailed attribute information can be found [here](https://resources.lendingclub.com/LCDataDictionary.xlsx)
<br><br>

**Company Goals**<br>
Increasing profit! But how can we achieve it? Some ways to increase profits are:
- Accepting applicants who will definitely pay off their loans
- Declining applicants who don't want to pay off the loan (potential to be defaulters)
<br><br>

**Problems**
- Credit risk is the possibility of a loss resulting from a borrower's failure to repay a loan or meet contractual obligations ([source](https://www.investopedia.com/terms/c/creditrisk.asp))
- When a lending company receives a loan application, the company has to make a decision whether the company will accept or decline based on the applicant's profile
- If the applicant is likely to pay off the loan but we don't approve their application, it may result in a loss of income for the company
- If the applicant is not likely to pay off the loan but we approve their application, it may result in financial loss for the company
<br><br>

**Objectives**
- Predict whether the borrower will pay off the loan or not
- Understanding the borrower behaviors:
  - What makes the borrower pay off the loan
  - What makes the borrower doesn't pay off the loan

## Exploratory Data Analysis

### What Happened?

The `Good` status is when the loan status is either `Current` or `Fully Paid`, otherwise the status is `Bad` (risky)

<img class="img-modal-src" src="project-lendingclub-loan-credit-risk/target-distribution.svg" alt="Target Distribution">

- There are 12% of borrowers who have a risky loan status
- Technically speaking, this dataset is an imbalanced dataset

### Who are The Borrowers?

<img class="img-modal-src" src="project-lendingclub-loan-credit-risk/employment-title-wordcloud.svg" alt="Employment Title Wordcloud">

- Many borrowers have the words `Manager`, `Service`, `Director`, `Assistant`, `Sale`, `Teacher`, or `Nurse` in their employment title
- Many borrowers didn't write their employment title, so it's marked as `Unknown`

### Why Did They Apply for a Loan?

<img class="img-modal-src" src="project-lendingclub-loan-credit-risk/loan-purpose-distribution.svg" alt="Loan Purpose Distribution">

- Most borrowers apply for loans for the purpose of debt consolidation

### What is Their Grade?

<img class="img-modal-src" src="project-lendingclub-loan-credit-risk/grade-distribution.svg" alt="Grade Distribution">

- Most borrowers have grade B and C

### Do Grades Matter?

<img class="img-modal-src" src="project-lendingclub-loan-credit-risk/grade-probability.svg" alt="Loan Status Probability by Grade">

- The grade feature has a natural order based on the loan status probability
- Grade A has the highest probability to have a good loan status.
- Grade G has the lowest probability to have a good loan status

### Loan Credit Risk Probability by Date Features

#### Issue Date

<img class="img-modal-src" src="project-lendingclub-loan-credit-risk/issue-date-probability.svg" alt="Loan Status Probability by Issue Date">

- The earlier the issue date is, the higher the probability of a borrower to have a bad loan status

#### Last Payment Date

<img class="img-modal-src" src="project-lendingclub-loan-credit-risk/last-payment-date-probability.svg" alt="Loan Status Probability by Last Payment Date">

- If the last payment has been made a long time ago, then the probability of a borrower to have a bad loan status will be higher

### Do Interest Rates Matter?

<img class="img-modal-src" src="project-lendingclub-loan-credit-risk/interest-rate-probability.svg" alt="Loan Status Probability by Interest Rate">

- Borrowers with high-interest rates have a higher probability to have a bad loan status than those with a low-interest rate

### Attribute Associations to Loan Status

I did some feature selection based on:
- Feature cardinality <br>
	Feature with high cardinality was dropped
- Feature associations
	Feature with very low association (almost zero) to loan status was dropped
- Multicollinearity & redundant values
	Drop one (or more) of the highly correlated features
<br>

Below is the attribute associations to loan status after feature selection

<img class="img-modal-src" src="project-lendingclub-loan-credit-risk/selected-feature-associations.svg" alt="Attribute Associations to Loan Status">

## Data Preprocessing

I do some data preprocessing, such as:
- Imputing missing values
- Removing redundant features
- Reducing feature skewness
- Feature extraction
- Feature transformation (encoding, scaling)
- Oversampling with SMOTE

## Model Development

I use XGBoost and LightGBM for model development. Below are the metric scores for the model with the default hyperparameter. For simplicity reason, I only show the accuracy, F1 score, and harmonic mean of accuracy and F1 score.
<br><br>
<style type="text/css">
#T_0f0b6_row0_col0 {
  background-color: #2685bb;
  color: #f1f1f1;
}
#T_0f0b6_row0_col1, #T_0f0b6_row1_col0 {
  background-color: #3d93c2;
  color: #f1f1f1;
}
#T_0f0b6_row0_col2 {
  background-color: #348ebf;
  color: #f1f1f1;
}
#T_0f0b6_row1_col1 {
  background-color: #589ec8;
  color: #f1f1f1;
}
#T_0f0b6_row1_col2 {
  background-color: #4e9ac6;
  color: #f1f1f1;
}
#T_0f0b6_row2_col0 {
  background-color: #c2cbe2;
  color: #000000;
}
#T_0f0b6_row2_col1 {
  background-color: #d2d2e7;
  color: #000000;
}
#T_0f0b6_row2_col2 {
  background-color: #cccfe5;
  color: #000000;
}
#T_0f0b6_row3_col0, #T_0f0b6_row3_col1, #T_0f0b6_row3_col2 {
  background-color: #fff7fb;
  color: #000000;
}
#T_0f0b6_row4_col0, #T_0f0b6_row4_col1, #T_0f0b6_row4_col2, #T_0f0b6_row5_col1, #T_0f0b6_row5_col2 {
  background-color: #023858;
  color: #f1f1f1;
}
#T_0f0b6_row5_col0 {
  background-color: #023b5d;
  color: #f1f1f1;
}
#T_0f0b6_row6_col0 {
  background-color: #034369;
  color: #f1f1f1;
}
#T_0f0b6_row6_col1 {
  background-color: #03466e;
  color: #f1f1f1;
}
#T_0f0b6_row6_col2 {
  background-color: #03456c;
  color: #f1f1f1;
}
#T_0f0b6_row7_col0 {
  background-color: #0a73b2;
  color: #f1f1f1;
}
#T_0f0b6_row7_col1 {
  background-color: #2182b9;
  color: #f1f1f1;
}
#T_0f0b6_row7_col2 {
  background-color: #187cb6;
  color: #f1f1f1;
}
#T_0f0b6_ th, #T_0f0b6_ td {
  border: none;
}
.lendingclub-table-body th {
  text-align: right;
}
</style>
<table id="T_0f0b6_" class="dataframe" style="width: auto">
  <thead>
    <tr>
      <th class="blank" >&nbsp;</th>
      <th class="blank level0" >&nbsp;</th>
      <th class="col_heading level0 col0" style="width: 20%">Accuracy</th>
      <th class="col_heading level0 col1" style="width: 20%">F1 Score</th>
      <th class="col_heading level0 col2" style="width: 20%">Harmonic Mean</th>
    </tr>
    <tr>
      <th class="index_name level0" style="text-align: right;">Model</th>
      <th class="index_name level1" style="text-align: right;">Feature Selection</th>
      <th class="blank col0" >&nbsp;</th>
      <th class="blank col1" >&nbsp;</th>
      <th class="blank col2" >&nbsp;</th>
    </tr>
  </thead>
  <tbody class="lendingclub-table-body">
    <tr>
      <th id="T_0f0b6_level0_row0" class="row_heading level0 row0" rowspan="4">XGBoost</th>
      <th id="T_0f0b6_level1_row0" class="row_heading level1 row0" >Without Feature Selection</th>
      <td id="T_0f0b6_row0_col0" class="data row0 col0" >0.950</td>
      <td id="T_0f0b6_row0_col1" class="data row0 col1" >0.809</td>
      <td id="T_0f0b6_row0_col2" class="data row0 col2" >0.874</td>
    </tr>
    <tr>
      <th id="T_0f0b6_level1_row1" class="row_heading level1 row1" >Feature Selection (75%)</th>
      <td id="T_0f0b6_row1_col0" class="data row1 col0" >0.946</td>
      <td id="T_0f0b6_row1_col1" class="data row1 col1" >0.799</td>
      <td id="T_0f0b6_row1_col2" class="data row1 col2" >0.866</td>
    </tr>
    <tr>
      <th id="T_0f0b6_level1_row2" class="row_heading level1 row2" >Feature Selection (50%)</th>
      <td id="T_0f0b6_row2_col0" class="data row2 col0" >0.923</td>
      <td id="T_0f0b6_row2_col1" class="data row2 col1" >0.741</td>
      <td id="T_0f0b6_row2_col2" class="data row2 col2" >0.822</td>
    </tr>
    <tr>
      <th id="T_0f0b6_level1_row3" class="row_heading level1 row3" >Feature Selection (25%)</th>
      <td id="T_0f0b6_row3_col0" class="data row3 col0" >0.902</td>
      <td id="T_0f0b6_row3_col1" class="data row3 col1" >0.695</td>
      <td id="T_0f0b6_row3_col2" class="data row3 col2" >0.785</td>
    </tr>
    <tr>
      <th id="T_0f0b6_level0_row4" class="row_heading level0 row4" rowspan="4">LightGBM</th>
      <th id="T_0f0b6_level1_row4" class="row_heading level1 row4" >Without Feature Selection</th>
      <td id="T_0f0b6_row4_col0" class="data row4 col0" >0.974</td>
      <td id="T_0f0b6_row4_col1" class="data row4 col1" >0.882</td>
      <td id="T_0f0b6_row4_col2" class="data row4 col2" >0.926</td>
    </tr>
    <tr>
      <th id="T_0f0b6_level1_row5" class="row_heading level1 row5" >Feature Selection (75%)</th>
      <td id="T_0f0b6_row5_col0" class="data row5 col0" >0.973</td>
      <td id="T_0f0b6_row5_col1" class="data row5 col1" >0.882</td>
      <td id="T_0f0b6_row5_col2" class="data row5 col2" >0.925</td>
    </tr>
    <tr>
      <th id="T_0f0b6_level1_row6" class="row_heading level1 row6" >Feature Selection (50%)</th>
      <td id="T_0f0b6_row6_col0" class="data row6 col0" >0.971</td>
      <td id="T_0f0b6_row6_col1" class="data row6 col1" >0.872</td>
      <td id="T_0f0b6_row6_col2" class="data row6 col2" >0.919</td>
    </tr>
    <tr>
      <th id="T_0f0b6_level1_row7" class="row_heading level1 row7" >Feature Selection (25%)</th>
      <td id="T_0f0b6_row7_col0" class="data row7 col0" >0.955</td>
      <td id="T_0f0b6_row7_col1" class="data row7 col1" >0.822</td>
      <td id="T_0f0b6_row7_col2" class="data row7 col2" >0.884</td>
    </tr>
  </tbody>
</table>
<br><br>
Overall, the LightGBM model performs better than the XGBoost model. What if we do some tuning for the hyperparameters?

## Model Optimization

I use Optuna for hyperparameter tuning. My tuning strategy:
- I don't want to get a high false negative rate, therefore I have to maximize the recall score
- However, I also don't want to get a high false positive rate, therefore I have to maximize the precision score as well
- To overcome these conditions, I will optimize the F1-score because it is the harmonic mean of precision and recall
- I use the F1-score from the negative class because I give more attention to optimizing the metrics for bad loan status
- I'm still paying attention to the accuracy score as well since this metric is easier to interpret

### XGBoost Tuned

<style type="text/css">
#T_1a46c_row0_col0, #T_1a46c_row2_col0, #T_1a46c_row2_col1, #T_1a46c_row6_col0, #T_1a46c_row6_col1 {
  background-color: #0a73b2;
  color: #f1f1f1;
}
#T_1a46c_row0_col1 {
  background-color: #2383ba;
  color: #f1f1f1;
}
#T_1a46c_row0_col2 {
  background-color: #1c7fb8;
  color: #f1f1f1;
}
#T_1a46c_row1_col0, #T_1a46c_row1_col1, #T_1a46c_row1_col2, #T_1a46c_row4_col0, #T_1a46c_row4_col1, #T_1a46c_row4_col2 {
  background-color: #023858;
  color: #f1f1f1;
}
#T_1a46c_row2_col2, #T_1a46c_row6_col2 {
  background-color: #0872b1;
  color: #f1f1f1;
}
#T_1a46c_row3_col0 {
  background-color: #f7f0f7;
  color: #000000;
}
#T_1a46c_row3_col1, #T_1a46c_row3_col2 {
  background-color: #f8f1f8;
  color: #000000;
}
#T_1a46c_row5_col0 {
  background-color: #03466e;
  color: #f1f1f1;
}
#T_1a46c_row5_col1 {
  background-color: #034165;
  color: #f1f1f1;
}
#T_1a46c_row5_col2 {
  background-color: #034267;
  color: #f1f1f1;
}
#T_1a46c_row7_col0, #T_1a46c_row7_col1, #T_1a46c_row7_col2 {
  background-color: #fff7fb;
  color: #000000;
}
#T_1a46c_ th, #T_1a46c_ td {
  border: none;
}
.lendingclub-table-body th {
  text-align: right;
}
</style>
<table id="T_1a46c_" class="dataframe" style="width: auto">
  <thead>
    <tr>
      <th class="blank" >&nbsp;</th>
      <th class="blank level0" >&nbsp;</th>
      <th class="col_heading level0 col0" style="width: 20%">Accuracy</th>
      <th class="col_heading level0 col1" style="width: 20%">F1 Score</th>
      <th class="col_heading level0 col2" style="width: 20%">Harmonic Mean</th>
    </tr>
    <tr>
      <th class="index_name level0" style="text-align: right;">Tuning Strategy</th>
      <th class="index_name level1" style="text-align: right;">Feature Selection</th>
      <th class="blank col0" >&nbsp;</th>
      <th class="blank col1" >&nbsp;</th>
      <th class="blank col2" >&nbsp;</th>
    </tr>
  </thead>
  <tbody class="lendingclub-table-body">
    <tr>
      <th id="T_1a46c_level0_row0" class="row_heading level0 row0" rowspan="4">Optimize F1 Score</th>
      <th id="T_1a46c_level1_row0" class="row_heading level1 row0" >Without Feature Selection</th>
      <td id="T_1a46c_row0_col0" class="data row0 col0" >0.969</td>
      <td id="T_1a46c_row0_col1" class="data row0 col1" >0.864</td>
      <td id="T_1a46c_row0_col2" class="data row0 col2" >0.913</td>
    </tr>
    <tr>
      <th id="T_1a46c_level1_row1" class="row_heading level1 row1" >Feature Selection (75%)</th>
      <td id="T_1a46c_row1_col0" class="data row1 col0" >0.974</td>
      <td id="T_1a46c_row1_col1" class="data row1 col1" >0.884</td>
      <td id="T_1a46c_row1_col2" class="data row1 col2" >0.927</td>
    </tr>
    <tr>
      <th id="T_1a46c_level1_row2" class="row_heading level1 row2" >Feature Selection (50%)</th>
      <td id="T_1a46c_row2_col0" class="data row2 col0" >0.969</td>
      <td id="T_1a46c_row2_col1" class="data row2 col1" >0.868</td>
      <td id="T_1a46c_row2_col2" class="data row2 col2" >0.916</td>
    </tr>
    <tr>
      <th id="T_1a46c_level1_row3" class="row_heading level1 row3" >Feature Selection (25%)</th>
      <td id="T_1a46c_row3_col0" class="data row3 col0" >0.956</td>
      <td id="T_1a46c_row3_col1" class="data row3 col1" >0.826</td>
      <td id="T_1a46c_row3_col2" class="data row3 col2" >0.886</td>
    </tr>
    <tr>
      <th id="T_1a46c_level0_row4" class="row_heading level0 row4" rowspan="4">Optimize Accuracy</th>
      <th id="T_1a46c_level1_row4" class="row_heading level1 row4" >Without Feature Selection</th>
      <td id="T_1a46c_row4_col0" class="data row4 col0" >0.974</td>
      <td id="T_1a46c_row4_col1" class="data row4 col1" >0.884</td>
      <td id="T_1a46c_row4_col2" class="data row4 col2" >0.927</td>
    </tr>
    <tr>
      <th id="T_1a46c_level1_row5" class="row_heading level1 row5" >Feature Selection (75%)</th>
      <td id="T_1a46c_row5_col0" class="data row5 col0" >0.973</td>
      <td id="T_1a46c_row5_col1" class="data row5 col1" >0.882</td>
      <td id="T_1a46c_row5_col2" class="data row5 col2" >0.925</td>
    </tr>
    <tr>
      <th id="T_1a46c_level1_row6" class="row_heading level1 row6" >Feature Selection (50%)</th>
      <td id="T_1a46c_row6_col0" class="data row6 col0" >0.969</td>
      <td id="T_1a46c_row6_col1" class="data row6 col1" >0.868</td>
      <td id="T_1a46c_row6_col2" class="data row6 col2" >0.916</td>
    </tr>
    <tr>
      <th id="T_1a46c_level1_row7" class="row_heading level1 row7" >Feature Selection (25%)</th>
      <td id="T_1a46c_row7_col0" class="data row7 col0" >0.955</td>
      <td id="T_1a46c_row7_col1" class="data row7 col1" >0.823</td>
      <td id="T_1a46c_row7_col2" class="data row7 col2" >0.884</td>
    </tr>
  </tbody>
</table>
<br><br>

### LightGBM Tuned

<style type="text/css">
#T_ee43b_row0_col0, #T_ee43b_row0_col1, #T_ee43b_row0_col2 {
  background-color: #023858;
  color: #f1f1f1;
}
#T_ee43b_row1_col0, #T_ee43b_row4_col0, #T_ee43b_row5_col0 {
  background-color: #034c78;
  color: #f1f1f1;
}
#T_ee43b_row1_col1, #T_ee43b_row4_col1 {
  background-color: #023d60;
  color: #f1f1f1;
}
#T_ee43b_row1_col2, #T_ee43b_row4_col2 {
  background-color: #034165;
  color: #f1f1f1;
}
#T_ee43b_row2_col0 {
  background-color: #045f95;
  color: #f1f1f1;
}
#T_ee43b_row2_col1, #T_ee43b_row6_col1 {
  background-color: #0568a3;
  color: #f1f1f1;
}
#T_ee43b_row2_col2 {
  background-color: #0566a0;
  color: #f1f1f1;
}
#T_ee43b_row3_col0 {
  background-color: #f4edf6;
  color: #000000;
}
#T_ee43b_row3_col1 {
  background-color: #f5eef6;
  color: #000000;
}
#T_ee43b_row3_col2 {
  background-color: #f4eef6;
  color: #000000;
}
#T_ee43b_row5_col1, #T_ee43b_row5_col2 {
  background-color: #034a74;
  color: #f1f1f1;
}
#T_ee43b_row6_col0 {
  background-color: #056dab;
  color: #f1f1f1;
}
#T_ee43b_row6_col2 {
  background-color: #0569a4;
  color: #f1f1f1;
}
#T_ee43b_row7_col0, #T_ee43b_row7_col1, #T_ee43b_row7_col2 {
  background-color: #fff7fb;
  color: #000000;
}
#T_ee43b_ th, #T_ee43b_ td {
  border: none;
}
.lendingclub-table-body th {
  text-align: right;
}
</style>
<table id="T_ee43b_" class="dataframe" style="width: auto">
  <thead>
    <tr>
      <th class="blank" >&nbsp;</th>
      <th class="blank level0" >&nbsp;</th>
      <th class="col_heading level0 col0" style="width: 20%">Accuracy</th>
      <th class="col_heading level0 col1" style="width: 20%">F1 Score</th>
      <th class="col_heading level0 col2" style="width: 20%">Harmonic Mean</th>
    </tr>
    <tr>
      <th class="index_name level0" style="text-align: right;">Tuning Strategy</th>
      <th class="index_name level1" style="text-align: right;">Feature Selection</th>
      <th class="blank col0" >&nbsp;</th>
      <th class="blank col1" >&nbsp;</th>
      <th class="blank col2" >&nbsp;</th>
    </tr>
  </thead>
  <tbody class="lendingclub-table-body">
    <tr>
      <th id="T_ee43b_level0_row0" class="row_heading level0 row0" rowspan="4">Optimize F1 Score</th>
      <th id="T_ee43b_level1_row0" class="row_heading level1 row0" >Without Feature Selection</th>
      <td id="T_ee43b_row0_col0" class="data row0 col0" >0.976</td>
      <td id="T_ee43b_row0_col1" class="data row0 col1" >0.892</td>
      <td id="T_ee43b_row0_col2" class="data row0 col2" >0.932</td>
    </tr>
    <tr>
      <th id="T_ee43b_level1_row1" class="row_heading level1 row1" >Feature Selection (75%)</th>
      <td id="T_ee43b_row1_col0" class="data row1 col0" >0.975</td>
      <td id="T_ee43b_row1_col1" class="data row1 col1" >0.891</td>
      <td id="T_ee43b_row1_col2" class="data row1 col2" >0.931</td>
    </tr>
    <tr>
      <th id="T_ee43b_level1_row2" class="row_heading level1 row2" >Feature Selection (50%)</th>
      <td id="T_ee43b_row2_col0" class="data row2 col0" >0.974</td>
      <td id="T_ee43b_row2_col1" class="data row2 col1" >0.883</td>
      <td id="T_ee43b_row2_col2" class="data row2 col2" >0.926</td>
    </tr>
    <tr>
      <th id="T_ee43b_level1_row3" class="row_heading level1 row3" >Feature Selection (25%)</th>
      <td id="T_ee43b_row3_col0" class="data row3 col0" >0.964</td>
      <td id="T_ee43b_row3_col1" class="data row3 col1" >0.851</td>
      <td id="T_ee43b_row3_col2" class="data row3 col2" >0.904</td>
    </tr>
    <tr>
      <th id="T_ee43b_level0_row4" class="row_heading level0 row4" rowspan="4">Optimize Accuracy</th>
      <th id="T_ee43b_level1_row4" class="row_heading level1 row4" >Without Feature Selection</th>
      <td id="T_ee43b_row4_col0" class="data row4 col0" >0.975</td>
      <td id="T_ee43b_row4_col1" class="data row4 col1" >0.891</td>
      <td id="T_ee43b_row4_col2" class="data row4 col2" >0.931</td>
    </tr>
    <tr>
      <th id="T_ee43b_level1_row5" class="row_heading level1 row5" >Feature Selection (75%)</th>
      <td id="T_ee43b_row5_col0" class="data row5 col0" >0.975</td>
      <td id="T_ee43b_row5_col1" class="data row5 col1" >0.889</td>
      <td id="T_ee43b_row5_col2" class="data row5 col2" >0.930</td>
    </tr>
    <tr>
      <th id="T_ee43b_level1_row6" class="row_heading level1 row6" >Feature Selection (50%)</th>
      <td id="T_ee43b_row6_col0" class="data row6 col0" >0.973</td>
      <td id="T_ee43b_row6_col1" class="data row6 col1" >0.883</td>
      <td id="T_ee43b_row6_col2" class="data row6 col2" >0.926</td>
    </tr>
    <tr>
      <th id="T_ee43b_level1_row7" class="row_heading level1 row7" >Feature Selection (25%)</th>
      <td id="T_ee43b_row7_col0" class="data row7 col0" >0.963</td>
      <td id="T_ee43b_row7_col1" class="data row7 col1" >0.848</td>
      <td id="T_ee43b_row7_col2" class="data row7 col2" >0.902</td>
    </tr>
  </tbody>
</table>
<br><br>

## Conclusion

## Explainable AI