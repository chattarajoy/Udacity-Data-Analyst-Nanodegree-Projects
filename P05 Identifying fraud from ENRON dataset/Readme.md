# Identifying Fraud from Enron Emails Dataset

#### *by Joy Lal Chattaraj*


## Case Study : Overview

>In 2000, Enron was one of the largest companies in the United States. By 2002, it had collapsed into bankruptcy due to widespread corporate fraud. In the resulting Federal investigation, a significant amount of typically confidential information entered into the public record, including tens of thousands of emails and detailed financial data for top executives.

## Short Questions

### Q1. Summarize for us the goal of this project and how machine learning is useful in trying to accomplish it. As part of your answer, give some background on the dataset and how it can be used to answer the project question. Were there any outliers in the data when you got it, and how did you handle those?<br/><br/>

>The goal of this project was to utilize the financial and email data from Enron to build a predictive that could identify whether an individual could be considered a "person of interest" (POI). The Enron corpus - publicly maed by US Federal Energy Regulatory Comission during its investgiation of Enron, which comprised of email and financial data of 146 people (records), most of which are senior management of Enron. The corpus is widely used for various machine learning problem and although it has been labeled aready, the value is the potential application for similar cases in other companies or spam filtering application. The dataset contained 146 records with 1 labeled feature (POI), 14 financial features, 6 email feature. Within these record, 18 were labeled as a "Person Of Interest" (POI).

>While trying to find outliers, I used the `matplotlib` library to plot the points on a scatter plot for fields `salary` and `bonus`. I found an outlier whose value was way higher than others. Upon further inestigation I figured out that the key for it was `TOTAL` which wasn't a valid data point for our dataset. I could figure out aonther outlier with an unusually long name when I was scanning throught the list of keys, it was `THE TRAVEL AGENCY IN THE PARK`.

>So, Outliers detected are:

* `TOTAL` action taken : key popped out from dictionary as it wasn't a valid datapoint
* `THE TRAVEL AGENCY IN THE PARK` : again I popped the key out of the dict for the same reason<br/><br/>

#### Q2. What features did you end up using in your POI identifier, and what selection process did you use to pick them? Did you have to do any scaling? Why or why not? As part of the assignment, you should attempt to engineer your own feature that does not come ready-made in the dataset -- explain what feature you tried to make, and the rationale behind it. In your feature selection step, if you used an algorithm like a decision tree, please also give the feature importances of the features that you use, and if you used an automated feature selection function like SelectKBest, please report the feature scores and reasons for your choice of parameter values.

> First of all I used `scikit-learn's` `MinMaxScaler` to scale the features, as many of the financial and email features varied over different ranges, it was important to scale them so that they are valued evenly.

