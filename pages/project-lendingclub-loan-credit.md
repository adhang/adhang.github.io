# LendingClub - Loan Credit Risk Prediction

This is my internship project as a data scientist at [id/x partners](https://idxpartners.com/)
<br><br>

In this project, I designed a predictive model to determine the probability that loan borrowers will have a good or bad (risky) loan status at a lending company with **98% accuracy**.
<br><br>

Note: This project is still on-going, will update later.

## Project Notebooks

I create separated notebooks due to my limited computing resources
- [Exploratory Data Analysis](https://github.com/adhang/learn-data-science/blob/main/LendingClub_Loan_Credit_EDA.ipynb)
- [Machine Learning Modeling](https://github.com/adhang/learn-data-science/blob/main/LendingClub_Loan_Credit.ipynb)

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

<img class="img-modal-src" src="project-lendingclub-loan-credit/target-distribution.svg" alt="Target Distribution">

- There are 12% of borrowers who have a risky loan status
- Technically speaking, this dataset is an imbalanced dataset

### Who are The Borrowers?

<img class="img-modal-src" src="project-lendingclub-loan-credit/employment-title-wordcloud.svg" alt="Employment Title Wordcloud">

- Many borrowers have the words `Manager`, `Service`, `Director`, `Assistant`, `Sale`, `Teacher`, or `Nurse` in their employment title
- Many borrowers didn't write their employment title, so it's marked as `Unknown`

### Why Did They Apply for a Loan?

<img class="img-modal-src" src="project-lendingclub-loan-credit/loan-purpose-distribution.svg" alt="Loan Purpose Distribution">

- Most borrowers apply for loans for the purpose of debt consolidation

### What is Their Grade?

<img class="img-modal-src" src="project-lendingclub-loan-credit/grade-distribution.svg" alt="Grade Distribution">

- Most borrowers have grade B and C

### Do Grades Matter?

<img class="img-modal-src" src="project-lendingclub-loan-credit/grade-probability.svg" alt="Loan Status Probability by Grade">

- The grade feature has a natural order based on the loan status probability
- Grade A has the highest probability to have a good loan status.
- Grade G has the lowest probability to have a good loan status

### Loan Credit Risk Probability by Date Features

#### Issue Date

<img class="img-modal-src" src="project-lendingclub-loan-credit/issue-date-probability.svg" alt="Loan Status Probability by Issue Date">

- The earlier the issue date is, the higher the probability of a borrower to have a bad loan status

#### Last Payment Date

<img class="img-modal-src" src="project-lendingclub-loan-credit/last-payment-date-probability.svg" alt="Loan Status Probability by Last Payment Date">

- If the last payment has been made a long time ago, then the probability of a borrower to have a bad loan status will be higher

### Do Interest Rates Matter?

<img class="img-modal-src" src="project-lendingclub-loan-credit/interest-rate-probability.svg" alt="Loan Status Probability by Interest Rate">

- Borrowers with high-interest rates have a higher probability to have a bad loan status than those with a low-interest rate

## Data Preprocessing

## Model Development & Evaluation

## Model Optimization

## Conclusion

## Explainable AI

## Model Deployment
