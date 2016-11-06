# Designing an A/B Test

> By Joy Lal Chattaraj

## Experiment Overview: Free Trial Screener

>At the time of this experiment, Udacity courses currently have two options on the home page: "start free trial", and "access course materials". If the student clicks "start free trial", they will be asked to enter their credit card information, and then they will be enrolled in a free trial for the paid version of the course. After 14 days, they will automatically be charged unless they cancel first. If the student clicks "access course materials", they will be able to view the videos and take the quizzes for free, but they will not receive coaching support or a verified certificate, and they will not submit their final project for feedback.

>In the experiment, Udacity tested a change where if the student clicked "start free trial", they were asked how much time they had available to devote to the course. If the student indicated 5 or more hours per week, they would be taken through the checkout process as usual. If they indicated fewer than 5 hours per week, a message would appear indicating that Udacity courses usually require a greater time commitment for successful completion, and suggesting that the student might like to access the course materials for free. At this point, the student would have the option to continue enrolling in the free trial, or access the course materials for free instead. This screenshot shows what the experiment looks like.

![jpg](img/screenshot.jpg)

>The hypothesis was that this might set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn't have enough time without significantly reducing the number of students to continue past the free trial and eventually complete the course. If this hypothesis held true, Udacity could improve the overall student experience and improve coaches' capacity to support students who are likely to complete the course.

>The unit of diversion is a cookie, although if the student enrolls in the free trial, they are tracked by user-id from that point forward. The same user-id cannot enroll in the free trial twice. For users that do not enroll, their user-id is not tracked in the experiment, even if they were signed in when they visited the course overview page.



## Experiment Design

### Metric Choice

*List which metrics you will use as invariant metrics and evaluation metrics here.*

>* Invariant Metrics : Number of cookies, Number of clicks
>* Evaluation Metrics : Gross Conversion, Net Conversion


*For each metric, explain both why you did or did not use it as an invariant metric and why you did or did not use it as an evaluation metric. Also, state what results you will look for in your evaluation metrics in order to launch the experiment.*


>* Number of cookies: This is a good invariant metric as it is calculated before the user views the experiment popup. So, the numbers would be similar in both control and experiment group. This explains why it cant't be a evaluation metric as it is not effected by the experiment.

>* Number of user-ids: This isn't an invariant metric as it is dependent on the user deciding wether to enroll after he receives the experiment popup, thus it is effected by our experiment. Numbers are not usually a good evaluation metrics, rates and probabilities can serve much better. So, I decided not to use it as an evaluation metric.

>* Number of clicks: Similar to the number of cookies, this value is independent from the experiment, so the number will be similar in experiment and control groups.Thus, this is a good invariant metric and not an evaluation metric.

>* Click-through-probability: This is a good invariant metric because it is independent from the experiment. However, I didn't choose this metric as an invariant metric for the test because this value seems to be redundant to the number of cookies and the number of clicks. This is not an evaluation metric as it doesn't change because of our experiment.

>* Gross Conversion: This is a good evaluation metric because it is dependent on the experiment (This explains why it cannot be a good invariant metric). We expect that the value will be lower in the experiment group because some people who are not able to commit more than 5 hours per week won't enroll the classes. In the control group, users won't see any pop-up message so they will enroll without any consideration of the number of hours they can commit per week.

>* Retention: This is a good evaluation metric because it is dependent on the experiment (This explains why it cannot be a good invariant metric). We expect this value will be higher in the experiment group because majority of the group are those who can commit 5 hours per week and these people are more likely to make the first payments for the classes. However, I didn't choose this as an evaluation metric for the test because it is redundant to Gross conversion and Net conversion; this value can be calculated using Retention and Net Conversion.

>* Net Conversion: This is a good evaluation metric because it is dependent on the experiment (This explains why it cannot be a good invariant metric). It would be great if this value increases after the test. However, due to the expected decrease in number of students enrolling the free trial, it is possible that net conversion might decrease after the test. However, since the majority of the experiment group are those who can commit 5 hours per week and they are more likely to make the first payments for the course. So we want this value doesn't decrease after the test.

### Measuring Standard Deviation

*List the standard deviation of each of your evaluation metrics.*


>* Gross Conversion : We Know S.E. = (p X (1 - p )/N)^1/2 
  Here : p = 0.20625
  N = (3200/40000)X5000
  
>  Thus, S.E = 0.0202

>* Net Conversion : p = 0.1093, N = (3200/40000)X5000

>  Thus, S.E. = 0.0156


*For each of your evaluation metrics, indicate whether you think the analytic estimate would be comparable to the the empirical variability, or whether you expect them to be different (in which case it might be worth doing an empirical estimate if there is time). Briefly give your reasoning in each case.*

>Gross Conversion and Net Conversion have the number of cookies as their denominators. Thus, the unit of diversion  is same as a unit of analysis. So, analytical estimate is comparable to the empirical variability.


### Sizing

#### Number of Samples vs. Power

*Indicate whether you will use the Bonferroni correction during your analysis phase, and give the number of pageviews you will need to power you experiment appropriately.*

>No, I will not use bonferroni correction. 

>Bonferroni correction is designed to reduce type 1 errors ( wherin one rejects the null when it is true) in those cases where we need *any* of our metrics to match the expectation not *all*.

>In our case it was just the opposite. We need *all* our metrics to meet our expectations or else the results aren't useful. So, it is better not to use Bonferroni correction as it would increase the chances of type 2 error (fail to reject the null when it is false.)


***Pageviews for Each Evaluation Metric to Achieve Target Statistical
Power***

>* Online Calculator used : http://www.evanmiller.org/ab-testing/sample-size.html

>#### Gross Conversion

>* Baseline Conversion: 20.625%
* Minimum Detectable Effect: 1% 
* Alpha: 5%
* dmin = 0.01
* Beta: 20% -Sensitivity (1 - Beta): 80% 
* Sample Size = 25,835 enrollments/group 
* Number of groups = 2 (experiment and control) 
* Total sample size = 51,670 enrollments 
* Clicks/Pageview: 3200/40000 = 0.08 clicks/pageview 
* Pageviews Required = 6,45,875

>#### Net Conversion

>* Baseline Conversion: 10.9313% 
* Minimum Detectable Effect: 0.75% 
* Alpha: 5% -Beta: 20% 
* Sensitivity (1 - Beta): 80% 
* dmin = 0.0075
* Sample size = 27,413 enrollments/group 
* Number of groups = 2 (experiment and control) 
* Total sample size = 54,826 enrollments 
* Enrollments/pageview: 3200/40000 = 0.08 clicks/pageview 
* Pageviews = 6,85,325

>*Pageviews required is maximum of pageviews required for Gross
Conversion, Retention, Net Conversion. Therefore, the required pageviews
is 6,85,325*

#### Duration vs. Exposure

*Indicate what fraction of traffic you would divert to this experiment and, given this, how many days you would need to run the experiment.* 

>The fraction of traffic I would divert to this experiment is 0.8 . 
>Given this fraction, I will need need ~ 22 days to run the experiment.

*Give your reasoning for the fraction you chose to divert. How risky do you think this experiment would be for Udacity?*

>Only 80% will be affected and the change due to the experiment is small, so it won't cause too much trouble in the overall business. The overall experiment is not very risky since there are no sensitive information we use in this experiment. Although users have to provide their credit card numbers when they enroll the course, these information are not part of the experiment.

> Thus, 22 days are enough to gather required data and the duration is reasonable, so we will run the experiment for 22 days.


### Experiment Analysis

#### Sanity Checks

*For each of your invariant metrics, give the 95% confidence interval for the value you expect to observe, the actual observed value, and whether the metric passes your sanity check.*

<table style="width:119%;">
<colgroup>
<col width="12%" />
<col width="23%" />
<col width="23%" />
<col width="23%" />
<col width="23%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="center">Metric</th>
<th align="center">Expected Value</th>
<th align="center">Observed Value</th>
<th align="center">CI Lower Bound</th>
<th align="center">CI Upper Bound</th>
<th align="center">Result</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="center">Number of Cookies</td>
<td align="center">0.5000</td>
<td align="center">0.5006</td>
<td align="center">0.4988</td>
<td align="center">0.5012</td>
<td align="center">Pass</td>
</tr>
<tr class="even">
<td align="center">Number of clicks on &quot;start free trial&quot;</td>
<td align="center">0.5000</td>
<td align="center">0.5005</td>
<td align="center">0.4959</td>
<td align="center">0.5042</td>
<td align="center">Pass</td>
</tr>
</tbody>
</table>


*For any sanity check that did not pass, explain your best guess as to what went wrong based on the day-by-day data. Do not proceed to the rest of the analysis unless all sanity checks pass.*

> All sanity checks passed.


### Result Analysis

#### Effect Size Tests

*For each of your evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant*

<table style="width:119%;">
<colgroup>
<col width="12%" />
<col width="23%" />
<col width="23%" />
<col width="23%" />
<col width="23%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="center">Metric</th>
<th align="center">dmin</th>
<th align="center">Observed Difference</th>
<th align="center">CI Lower Bound</th>
<th align="center">CI Upper Bound</th>
<th align="center">Result</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="center">Gross Conversion</td>
<td align="center">0.01</td>
<td align="center">-0.0205</td>
<td align="center">-.0291</td>
<td align="center">-.0120</td>
<td align="center">Satistically and Practically Significant</td>
</tr>
<tr class="even">
<td align="center">Net Conversion</td>
<td align="center">0.0075</td>
<td align="center">-0.0048</td>
<td align="center">-0.0116</td>
<td align="center">0.0019</td>
<td align="center">Neither Statistically nor Practically Significant</td>
</tr>
</tbody>
</table>

### Sign Tests

*For each of your evaluation metrics, do a sign test using the day-by-day data, and report the p-value of the sign test and whether the result is statistically significant.*

<table>
<thead>
<tr class="header">
<th align="center">Metric</th>
<th align="center">p-value for sign test</th>
<th align="center">Statistically Significant @ alpha .05?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="center">Gross Conversion</td>
<td align="center">0.0026</td>
<td align="center">Yes</td>
</tr>
<tr class="even">
<td align="center">Net Conversion</td>
<td align="center">0.6776</td>
<td align="center">No</td>
</tr>
</tbody>
</table>



### Summary

*State whether you used the Bonferroni correction, and explain why or why not. If there are any discrepancies between the effect size hypothesis tests and the sign tests, describe the discrepancy and why you think it arose.*

>I didn't use Bonferroni correction because the metrics are not independent. 

>Bonferroni correction is designed to reduce type 1 errors ( wherin one rejects the null when it is true) in those cases where we need *any* of our metrics to match the expectation not *all*.

>In our case it was just the opposite. We need *all* our metrics to meet our expectations or else the results aren't useful. So, it is better not to use Bonferroni correction as it would increase the chances of type 2 error (fail to reject the null when it is false.)

>Both effect size tests and sign tests result in having statistical significance in Gross Conversion but no statistical significance in Net Conversion. This means that although the experiment affects the users' decision to enroll the online courses but it didn't affect much to the enrolled users to pay the courses.




### Recommendation

*Make a recommendation and briefly describe your reasoning.*

>I would recommend not to launch the experiment. The result of Gross Conversion showed statistically and practically significant changes after the pop-up message. This means that only those who are likely to commit more than 5 hours per week enroll the classes and they are more likely to make the first payments; this will reduce the costs of having those who are only taking free courses without making any payment. However, Net Conversion don't show statistically or practiclly significant changes after the test. This means that showing pop-up message to users before they enroll the classes don't affect the number of users who make their first payments after the free trial. Furthermore, the confidence interval of the net conversion includes the negative of the practical significance boundary which suggests the risk of hurting the Udacity's businiess.


### Follow-Up Experiment

*Give a high-level description of the follow up experiment you would run, what your hypothesis would be, what metrics you would want to measure, what your unit of diversion would be, and your reasoning for these choices.*

>A follow-up experiment could be based upon motivation with only a slight change from the previous experiment. It would require a method to approximate the number of hours that each student dedicated to the material in the first week. If a student committed less than the recommended number of hours, a message would pop-up upon login before the start of the second week to motivate the student to commit more time by showing success stories of students who have already completed the nanodegree.Those that met the recommended number of hours wouldn't get a direct message but could still access this repository of interviews from their course homepage under the 'Resources' tab.

> My hypothesis is is that the message would motivate some students who might otherwise drop out during the 14-day trial to continue past and possibly complete the course. It would also not affect those people that would otherwise continue through the trial and complete the course had there been no pop-upmessage. In this case,the overall student experience in the forums could be more energized and improve beyond the first week,and coaching resources would be used on more enthusiastic and dedicated students.
Considering this design, retention rate would be the best way to test our hypothesis*(Evaluation metric is Retention Rate)*. Being that we would divert traffic evenly among the control and experimental groups, the most suitable *invariant metric* would be the number of user-id's to complete checkout and enroll in the course. It would be practical at this point, to divert students into the control or experiment group *(Unit of Diversion is user-id)*. It's worth noting that this experiment would likely take longer to conduct.