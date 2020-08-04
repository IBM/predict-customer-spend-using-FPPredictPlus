# Introduction 

**This tutorial is part of a series on Red Hat Marketplace operator FP Predict Plus. Please refer to the `Prerequisites` section for `Getting Started`.**

### How to build a Machine Learning Regression model using FP Predict Plus

**`Machine learning`** is a large field of study that overlaps with and inherits ideas from many related fields such as artificial intelligence. The focus of the field is learning, that is, acquiring skills or knowledge from experience. Most commonly, this means synthesizing useful concepts from historical data. As such, there are many different types of learning that you may encounter as a practitioner in the field of machine learning from whole fields of study to specific techniques.

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

**Note :- Only `csv` format is supported and the dataset need to have a column with unique values. In these csv files, we have added a `Row_num` column to be unique. The datasets needs to be split into training, testing and holdout (validation) datasets before hand.** `Citation is needed to use these datasets for other projects.`


### Create a job

We need to create a new `job` in the platform. Click on `Dashboard` which is the first option on the left navigation pane and hit `Start` on the top right hand side.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/job-strt.png)

We need to click on `No` as our data does not contain Date or Timestamps. The platform will understand to create a `Predict` job with no Date or Timestamps and if the dataset has Date or Timestamps, then platform will create a `Forecast` job.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/job-sel.png)

Lets go ahead and create a new job by filling in the details per below. We will update the name, select the task as `Model + Predict` as that is what we will be doing. We can select `Model` and it will build a model for us and select `Predict` if we have a model file ready for doing predictions. Set the dataset location to `Cloud` and select the train and test datasets using `Browse` for upload. Select the Target Variable as `Spend` and Unique Identifier as `Row_num`. Under `Advanced settings`, Operation Mode should be set to `Automated`. Hit `Run` to get the job started.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/crt-job.png)

The job will take a couple of minutes to complete. We can observe how many models are getting created and the different scenarios evaluated in the process. 

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/job-rng.png)

`Note` :- The regression model will take a little longer to complete when compared with a binary classification model.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/crtd-mdls.png)

The model will try to use different scenarios like all variables/few variables etc for generating predictions. We should see the job status per below.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/job-complete.png)

### Review the job details

Lets review the job which has been created for us by clicking on `Dashboard` which is the first option on the left navigation pane and select the job with name `build-model`. The `number` preceding before the job name is to identify how many jobs have run so far and can be ignored. We can observe the model distribution where model `M-9` has scored for 23 records in the test data and model `M-3 & M-5` have scored for one record each in the test data. 

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/view-job.png)

We can observe the complete job details like `Description`, `Modelling` and `Prediction`. The system built 7 models using 479 records from the training data in 290 seconds and generated predictions on 25 records from testing data.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/job-dtls.png)

### Analyze results

Lets review the model performance in detail. Click on `Predicted vs Actual` option to see the model performance. We can observe that predicted values are very close to actual values. The model was able to learn from the data and generated predictions with good accuracy. 
`Note` :- It was observed that the model is sensitive towards outliers in the dataset. We can deal with outliers in different ways by identifying the root cause and exclude them if necessary. We can also retain outliers in the dataset for further analysis and treat them accordingly. 

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/prd-act.png)

Click on `Models` to understand how many predictions are done by each model. We can observe that model `M-9` has scored for 23 records from the testing data.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/mdls.png)

Click on `Variables` to understand the significance of each variable in predicting the outcome. We can observe that all variables except `LoanAmount` were used by most of the models.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/variables.png)

Click on `Variables of Models` to understand different scenarios explored by different models. We can observe that models `M-3` and `M-9` used all variables where as `M-5` used ten variables for building different models. 

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/scenarios.png)

### Download the Results & Model file

We can download the results which has all the model details mentioned above for further analysis. Lets go ahead and click on `Download Results` and `Download Model File` under `Download Files` option and save them in your local system. The `Results` file is named as `build-model-report` and the `model file` is named as `build-model-file.models`. 

In the `Results` file under the tab `Prediction Result`, we can see the model performance where the Mean Absolute Percentage Error (MAPE) is 5.59% which means the model accuracy is ~ 94%. These results are great given that we have used relatively smaller datasets. We can also review other details of the model in the excel file. 

The `Results` and `Model File` for this experiment are also available in this repo under `reports` and `model` folders. The `Model file` can be uploaded onto cloud using the `Dataset Management` option as described earlier.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/dnld-r-m.png)

### Prediction using new data

In this section, we will learn how to do predictions using the model on new dataset. We will be using the `saved model` from previous step to generate predictions using new records from the `holdout data`. The hold out data file will need to have target variable column `Spend` (without any values) failing which the system prompts an error stating `headers do not match between the training data and the holdout data`. 

### Create predict job

Lets create a new job for prediction by clicking on `Dashboard` option in the left navigation pane and hit `Start`. Update the `job name`, `description`, select `Predict` under `Tasks` as we have already built the model in previous steps. Upload the `model file` and `holdout data` from `cloud or local` whichever is convenient for you and select `Unique Identifier` as `Row_num`.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/gen-pred.png)

The predict job will start per below. We should get a message stating `Job Completed Successfully` in couple of minutes.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/scoring-job.png)

### Check job summary

Lets look at job summary by clicking `Dashboard` and selecting `generate-predictions` job. We can observe that, models `M-3 & M-9` have scored for two records each in the holdout data.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/prd-job.png)

### Analyze results of predict job

We can get more details in the next step where we can observe that prediction was made on all four records from the holdout dataset and the trained model file has used 479 records for building seven models. 

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/gen-pred-dtls.png)

`Note` :- `Predicted vs Actual` option is not clickable because there's no actual value to be compared. We have generated predicted values given a set of input parameters. We can review `Models, Variables & Variables of Models` as part of model evaluation.

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/prd-job-varbles.png)

### Download predicted results

We can get all the details about model performance by clicking on `Download Results` under `Download Files` option per below. 

![](https://github.com/IBM/build-a-regression-model-using-fppredictplus/blob/master/images/prd-res.png)

**In the file under `Predicted Result` tab, we can observe four values under `Predicted Value` which are the generated predictions for the holdout data. The `Results` file by name `generated-predictions-report` is also available under `reports` folder for reference.**

# Summary

With this, we have come to an end of this tutorial. We have learnt how to use FP Predict Plus platform for building AI models using `Regression` technique and also explored how to generate predictions on the new dataset. This platform will be extremly beneficial for developers, data scientists to build AI solutions quickly under different domains.

# Related Links

[Click here to know more about FP Predict Plus](https://marketplace.redhat.com/en-us/products/fp-predict)

[Click here to know more about Red Hat Marketplace](https://marketplace.redhat.com/en-us)

# Citation for data :

The dataset which is referenced in this tutorial is prepared by R.K.Sharath Kumar, Data Scientist, IBM India Software Labs.
