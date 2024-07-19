# Key findings: People with the highest credit score, and have a co-applicant, are more likely to receive a large loan amount.


## Table of Contents

  - [Business problem](#business-problem)
  - [Data source](#data-source)
  - [Methods](#methods)
  - [Tech Stack](#tech-stack)
  - [Quick glance at the results](#quick-glance-at-the-results)
  - [Lessons learned and recommendation](#lessons-learned-and-recommendation)
  - [Limitation and what can be improved](#limitation-and-what-can-be-improved)
  - [Run Locally](#run-locally)
  - [Explore the notebook](#explore-the-notebook)
  - [Deployment on streamlit](#deployment-on-streamlit)
  - [App deployed on Streamlit](#app-deployed-on-streamlit)
  - [Repository structure](#repository-structure)
  - [Contribution](#contribution)
  - [License](#license)




## Business problem

This app predicts how much of a loan will be granted to an applicant. The app uses different information about the applicant profile and predict how much will be approved. Usually the applicant with a higher credit score, a co-applicant will be granted a larger loan amount. It depends also on how much the applicant has requested.
## Data source

- [Kaggle loan amount prediction](https://www.kaggle.com/phileinsophos/predict-loan-amount-data)

## Methods

- Exploratory data analysis
- Bivariate analysis
- Multivariate correlation
- S3 bucket model hosting
- Model deployment
## Tech Stack

- Python (refer to requirement.txt and yml file in the assets folder for the packages used in this project)
- Streamlit (interface for the model)
- AWS S3 (model storage)


## Quick glance at the results

Correlation between the features.

![heatmap](https://github.com/aryan-norbert/Loan-Amount-Prediction/blob/main/heatmap.png)

RMSE of random forest with the best hyperparameters.

![RMSE](https://github.com/aryan-norbert/Loan-Amount-Prediction/blob/main/rmse.png)
We have an RMSE on a range between 0 and 400000

Top features of random forest with the best hyperparameters.

![Top 10](https://github.com/aryan-norbert/Loan-Amount-Prediction/blob/main/top10.png)

Least useful features of random forest with the best hyperparameters.

![Bottom 10](https://github.com/aryan-norbert/Loan-Amount-Prediction/blob/main/bottom10.png)

Top 3 models (with default parameters)

| Model with the best hyperparameter     	                | RMSE (range between 0 and 400000) 	|
|-------------------	                                    |------------------	|
| Random Forest      	                                    | 20791.86 	            |
| Bagging   	                                            | 20780.02 	            |
| Gradient Boosting               	                        | 26974.42	            |


- ***The final model used is: Random Forest***
- ***Metrics used: RMSE***
- Why choose random forest while bagging yield the best results?:
Comparing the RMSE while tuning the parameters, random forest produced the lowest RMSE constitenly.


    RMSE random forest

    ![RMSE random forest](https://github.com/aryan-norbert/Loan-Amount-Prediction/blob/main/rmse_rand_forest.png)

    RMSE bagging

    ![RMSE bagging](https://github.com/aryan-norbert/Loan-Amount-Prediction/blob/main/rmse_bagging.png)



## Lessons learned and recommendation

- Based on the analysis on this project, we found out that the loan amount that will be granted is determined mainly by the loan amount requested, credit score and a co-applicant. The least important features are expenses types and gender.
- Recommendation would be to focus more on the most predictive feature when looking at the applicant profile, and pay less attention on the least predictive features.
## Limitation and what can be improved

- The dataset lack a metadata about the features. (What expenses types mean? What does property type 1, 2, 3, 4 mean?)
- Retrain the model without the least predictive features
- Hyperparameter tuning: I used RandomSearchCV to save time but could be improved by couple of % with GridSearchCV.


## Run Locally
Initialize git

```bash
git init
```


Clone the project

```bash
git clone https://github.com/semasuka/Loan-amount-prediction-regression.git
```

enter the project directory

```bash
cd Loan-amount-prediction-regression
```

Create a conda virtual environment and install all the packages from the environment.yml (recommended)

```bash
conda env create --prefix <env_name> --file assets/environment.yml
```

Activate the conda environment

```bash
conda activate <env_name>
```

List all the packages installed

```bash
conda list
```

Start the streamlit server locally

```bash
streamlit run loan_amount_app.py
```
If you are having issue with streamlit, please follow [this tutorial on how to set up streamlit](https://docs.streamlit.io/library/get-started/installation)

## Explore the notebook

To explore the notebook file [here](https://nbviewer.org/github/semasuka/Loan-amount-prediction-regression/blob/main/Loan_amount_prediction.ipynb)

## Deployment on streamlit

To deploy this project on streamlit share, follow these steps:

- first, make sure you upload your files on Github, including a requirements.txt file
- go to [streamlit share](https://share.streamlit.io/)
- login with Github, Google, etc.
- click on new app button
- select the Github repo name, branch, python file with the streamlit codes
- click advanced settings, select python version 3.9 and add the secret keys if your model is stored on AWS or GCP bucket
- then save and deploy!

## App deployed on Streamlit

![Streamlit GIF](assets/gif_streamlit.gif)

Video to gif [tool](https://ezgif.com/)
## Repository structure


```

├── assets
│   ├── bottom10.png                              <- A picture of the bottom 10 features
│   ├── environment.yml                           <- list of all the dependencies with their versions(for conda environment)
│   ├── gif_streamlit.gif                         <- gif file used in the README
│   ├── heatmap.png                               <- heatmap image used in the README
│   ├── loan_amount_banner.png                    <- banner image used in the README
│   ├── rmse.png                                  <- Image of the best RMSE from the random forest used in the README
│   ├── rmse_bagging.png                          <- Image of the bagging RMSE used in the README
│   ├── rmse_rand_forest.png                      <- Image of the random forest RMSE used in the README
│   ├── top10.png                                 <- A picture of the top 10 features
│
├── datasets
│   ├── test.csv                                  <- the test data
│   ├── train.csv                                 <- the train data
│
│
├── .gitignore                                    <- used to ignore certain folder and files that won't be commit to git.
│
│
├── Loan_amount_prediction.ipynb                  <- main python notebook where all the analysis and modeling are done.
│
│
├── README.md                                     <- this readme file.
│
│
├── loan_amount_app.py                            <- file with the model and streamlit component for rendering the interface.
│
│
├── requirements.txt                              <- list of all the dependencies with their versions(used for Streamlit).

```
## Contribution

Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change or contribute.


