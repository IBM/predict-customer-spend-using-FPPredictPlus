# Introduction 

**This tutorial is part of a series on Red Hat Marketplace operator FP Predict Plus. Please refer to the `Prerequisites` section for `Getting Started`.**

### How to build a Machine Learning Regression model using FP Predict Plus

**`Machine learning`** is a large field of study that overlaps with and inherits ideas from many related fields such as artificial intelligence. The focus of the field is learning, that is, acquiring skills or knowledge from experience. Most commonly, this means synthesizing useful concepts from historical data. As such, there are many different types of learning that you may encounter as a practitioner in the field of machine learning: from whole fields of study to specific techniques.

**`Regression`** in machine learning and statistics is a supervised learning approach in which the computer program learns from the data given to it and make new observations or predictions. In this technique, the target variable has continuous values ranging from zero to infinity. 

Examples of regression problems include:

* Given historical data, predict the temperature
* Given historical data, predict the sales
* Given historical data, predict the house price

We will be using **`FP Predict Plus operator` from `Red Hat Marketplace`** to solve this usecase. Please refer to the content under `Related Links` section to know more about `FP Predict Plus operator` and `Red Hat Marketplace`.

# Prerequisites

We need to install and set up the `FP Predict Plus operator on Open Shift cluster` as per the instructions given below. 

[Install and setup FP Predict Plus operator on Red Hat Marketplace](https://github.com/IBM/getting-started-with-fppredictplus)

# Estimated time

It should take about 30-45 minutes to complete this tutorial. 

# Steps

### Add the data

Launch the FP Predict Plus platform and sign in using the default credentials. Lets begin by adding `datasets`. Clone this repo and navigate to `data` folder to download the datasets onto your local file system. 

Click on `Dataset Management` which is the third option on the left navigation pane and select `Datasets` on the top. 

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/add-data.png)

Click on `Browse` and select the three csv files for upload. The datasets gets uploaded to the platform in a minute. The upload time is dependent on the size of the datasets. 

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/data.png)

**Note :- Only `csv` format is supported and the dataset need to have a column with unique values. In these csv files, we have added a `Count` column to be unique. The datasets needs to be split into training, testing and holdout (validation) datasets before hand.** `Citation is needed to use these datasets for other projects.`

### Generate API Key

We need to generate an API key to access the `FP Predict Plus operator instance` for submitting the jobs. Launch the instance and click on `License Information` tab on the left navigation pane and click on `generate` under `API Key` section. Copy the API key to be used in next steps.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/gen-api-key.png)

### Create a job


