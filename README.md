# ScoreConflow
version:20240803

WeChat consultation  
![WeChat consultation](wechat_scf.png)

[Welcome to download and use ScoreConflow_20240803](ScoreConflow_20240803.zip)

#### Product Introduction

An AI-generated scorecard model. Version 20240803 of ScoreConflow.
ScoreConflow is composed of three words: ScoreCard Configuration Flow.
As each word means, ScoreConflow uses text to allow users to configure all business-related AI interaction instructions at one time, and automatically converts user instructions into code to generate a scorecard.
Its concept is that business is model and data is model. Users only need to set AI interaction instructions related to business data in text files, and leave the complex and time-consuming modeling work to ScoreConflow, so that they can focus all their energy on business and data.
While it is running, users do not need to be on duty. After ScoreConflow is finished, they can get professional-level models and reports, saving users the trouble of writing reports.

#### Product Highlights

1. Users do not need to write program code, they can achieve 100% customization of complex business through text interaction. The purpose of this product is not to provide a black box fool-style scorecard production product, but to provide users with a modeling tool that can improve work efficiency and improve model accuracy compared to existing products, so that users can focus on business and data.
2. The binning algorithm built into SCF is truly optimal binning. The optimal binning of other products refers to chi-square binning, tree binning and other methods that are different from equal frequency binning. The optimal binning of SCF is a mathematically provable global optimal analytical solution. The segmentation it gives can maximize IV, and it can be mathematically proven to be the upper limit of all binning methods. Under the conditions of the number of bins, percentage threshold and minimum gain specified by the user, it is still possible to calculate the binning node that meets the highest IV set by the user.
3. When binning, you can specify the binning shape, that is, specify whether the binning is monotonically increasing, monotonically decreasing, U-shaped, or inverted U-shaped. When the shape is specified, the optimal binning of SCF is still a mathematically provable global optimal analytical solution, and is the binning method with the highest IV under the same conditions.
4. When the user is unsure of the binning conditions, SCF will give an optimal suggestion from monotonically increasing, monotonically decreasing, U-shaped, and inverted U-shaped.
5. Among other scorecard modeling tools that I have tried, only OptBinning can support specifying bin shapes. However, the IV value of its bins is significantly smaller than that of SCF bins.
6. Different from the existing two-way stepwise regression, the built-in two-way stepwise regression algorithm of SCF can support users to set conditions, such as the sign of variable coefficients, variables that must be included in the model, and the use of other model evaluation indicators to screen variables.
7. After writing the AI interaction file, you can run it with one click without any on-call work. After the run, a very professional model report will be automatically generated. The intermediate results will also be saved as pkl for advanced users to make further customized development.
8. Provide a variety of services for users with different needs, support one-click fully automated operation, can independently call the optimal binning and bidirectional stepwise regression algorithms that have been optimized and enhanced in accuracy, and support semi-automated operation (modify the intermediate results of fully automated operation)
    
Note: This product has many advantages, and the author has been using it to complete modeling work. The author can improve work efficiency by 4 times, and the output model results are better. The product supports a lot of functions, and users can only experience its convenience, efficiency and accuracy by using it in person.

#### Who needs to use it

If you are suffering from the following problems:
1. Each time you develop a scorecard, you have to maintain a large amount of repetitive code or operate complex graphical configurations.
2. You don’t want to write a single line of code, but need to process complex data logic.
3. There are more and more variables, the binning shape given by automatic binning conflicts with the business, the workload of manually adjusting the binning is large, and the IV value drops a lot.
4. The variables or variable coefficients given by ordinary two-way stepwise logistic regression conflict with the business. Manually adjusting the input variables and repeatedly modeling is time-consuming and laborious, and the model indicators are greatly reduced.
5. Don’t want to wait for a long time for the program to run.
6. Spend a lot of time compiling model reports.
7. You need to read a lot of code to trace back the details of model construction.
8. Users who want to further improve the rating effect.
9. Users who spend too much time on work.
        
Then you should try ScoreConflow. Users only need to tell SCF the data and business requirements used for modeling through text, and it will automatically generate the optimal scorecard model, that is, the one with the highest bin IV and the highest model index.


#### Example
Through a simple example, we can feel how convenient ScoreConflow is to use.
    
1. Write conf.txt with the following content:
[PROJECT CONFIG]
model_name = Test
[DATA CONFIG]
model_data_file_path = ../Test/data

2. Double-click to run ScoreConflow/CMD/scf.cmd and follow the prompts to enter the location of conf.txt.
After a short wait, you can get a professional scorecard model development report.

#### Comparison with OptBinning's binning IV
OptBinning is the most downloaded scorecard development tool to date. Some people have compared the IV values of OptBinning binning with those of ScoreConflow binning.
For the detailed comparison process, please click on the title to view the original text
[OptBinning and ScoreConflow binning IV comparison](https://zhuanlan.zhihu.com/p/713158084)
![OptBinning vs. ScoreConflow binning IV comparison](https://gitee.com/ScoreConflow/scf_20240803/raw/master/IV%20OPT%20SCF.png)

#### Introduction to AI instruction set
There are 63 instruction sets in total to help users complete the development of complex scorecards, among which the model name and training dataset location must be set.
Introduce several important instruction sets:
1. In addition to the training set and test set, psi_data_file_path and oot_data_file_path can also specify psi, oot and other datasets. The performance of the model on psi, oot and other datasets will be written into the model report. The psi dataset can also be used for feature filtering.
2. order_cate_vars and unorder_cate_vars specify ordered and unordered categorical variables. SCF automatically handles categorical variables, and the binning of categorical variables is also a mathematically provable global optimal analytical solution, that is, the IV is the highest among all binning nodes.
3. Monotony constraint of the mono variable. Value range:
N: IV value is the highest globally, no constraints
A: According to all the data in model_data_file_path, a constraint is automatically selected from L+, L-, Uu, Un. Under this constraint, the IV value is the highest globally.
L: The IV value is globally the highest under linear monotone constraints (automatically determines L+, L-)
L+: The IV value is globally the highest under the linear monotonically increasing constraint
L-: The IV value is globally the highest under the linear monotonically decreasing constraint
U: The IV value is the highest globally under the U-type constraint (automatically determines Uu, Un)
4.spec_comb_policy automatically handles special values with too small a distribution ratio. Value range:
A:auto finds the closest eventProb among all values
a:auto only finds the closest eventProb among non-special values
F:first merges with the first bin of non-special values
L:last merges with the last bin of non-special values
M:median merges with the middle bin of non-special values (if there are an even number of bins, merge with the bin with the high event rate)
m:median merges with the middle bin of non-special values (if there are an even number of bins, merge with the bin with a low event rate)
B: max_Probability is merged with the bin with the largest eventProb
S:min_Probability merges with the bin with the smallest eventProb
5. measure_index In bidirectional stepwise regression, it is used to determine whether the model has been improved. Different indicators should be used for different application modes of the model. Value range:
aic, bic, roc_auc, ks, lift_n (under development), ks_price (under development)
6. measure_data_name In bidirectional stepwise regression, determine whether the model has an improved data set. This concept is the same as the concept of introducing out-of-bag data in random forest and xgboost.
7. pvalue_max, vif_max, corr_max, coef_sign: restrict the pvalue, vif, corr and coefficient sign of the model input variable respectively. If the user's restrictions are not met, the variable will not be introduced even if the model index is improved. This can make the model test and model building go on simultaneously, avoid repeated modeling, and save users' time.
For the full set of instructions and detailed explanation, see conf.txt
    
#### Installation Tutorial

Download ScoreConflow_20240803.zip, unzip it and open "Docs\xx\03_Installation Method.docx" to view it.
xx is your country code

#### Instructions

Download ScoreConflow_20240803.zip, unzip it and open "Docs\xx\05_Instructions.docx" to view it.
xx is your country code

#### API
    
The API is mainly for advanced users. If you do not need to use ScoreConflow to generate models directly, but need to use the powerful functions of the built-in components in ScoreConflow, you can read the API to get the usage of the built-in components.
Since ScoreConflow is designed to be pluggable, advanced users can use these built-in component modules separately like any Python module.
Download ScoreConflow_20240803.zip, unzip it and open "Docs\xx\06_API.docx" to view it.
xx is your country code


#### Introduction to main modules
##### 1.CardFlow

Implement a set of fixed processes (see Competitive Product Comparison - Built-in Fixed Workflow). It divides the scorecard development process into 10 stages:
Data reading, equal frequency binning, feature pre-screening, monotonic and U-shaped recommendations, optimal binning, WOE conversion, feature screening, model building, scorecard creation, and report generation.
The results will be automatically saved after each stage is completed. You can resume or update the previous results from any stage, and the results of the steps that have been calculated will not be lost when the computer is restarted.
For example: cardflow.start(start_step=1,end_step=10) executes all steps.
After execution, if you change the configuration file, such as changing the feature filtering conditions, which affects the results of step 7 and later, you need to update 7-10. In this case, just execute:
Just use cardflow.start(start_step=7,end_step=10). The previous results do not need to be re-executed.
For most users, once the configuration file is configured, CardFlow is the only component you need to interact with.
The interaction method is very simple: cardflow.start(start_step=a,end_step=b)
##### 2.Bins

Calculate the optimal split point for binning. The optimal split point calculated by Bins is a global optimal analytical solution with mathematical proof.
For categorical variables, including ordered and unordered categories, the global optimal analytical solution with mathematical proof can also be calculated.
Its main functions are:
1. The global optimal solution can be found under unconstrained or constrained conditions. Constraints supported: monotonic constraints (automatically determine increasing or decreasing), monotonic decreasing constraints, monotonic increasing constraints, U-shaped constraints (automatically determine convex or concave), and automatically set appropriate constraints (automatically determine monotonic decreasing constraints, monotonic increasing constraints, U-shaped constraints convex, and U-shaped constraints concave).
2. Find the global optimal solution for ordered categorical variables under constraints.
3. Use "minimum difference in event rates between adjacent bins" instead of "information gain" or "chi-square value" to suppress the formation of bins with too small differences. Users can intuitively feel the size of the difference between bins. Categorical variables also support this function.
4. Do not replace the minimum value of the first bin with negative infinity, and do not replace the maximum value of the last bin with positive infinity. The significance of this is that the ignored abnormal values will not be covered up due to the extension of extreme values to infinity. At the same time, ScoreConflow provides a complete mechanism to deal with the problem of online values exceeding the modeling boundary value. This solves the common contradiction between discovering special values as early as possible during data analysis and covering up special values during online applications (but with timely warnings).
5. Introduce the concept of wildcards to solve the problem that the online values of categorical variables exceed the modeling range.
6.Support multi-process parallel computing.
7. Support binning of weighted samples.
In most cases, users do not need to interact directly with Bins components. Since ScoreConflow is designed to be pluggable, advanced users can use Bins modules separately like any python module.
##### 3.Reg_Step_Wise_MP

It is a linear two-way stepwise regression and logistic two-way stepwise regression implemented in Python, which adds the following features compared to traditional two-way stepwise regression:
1. When performing stepwise variable selection for logistic regression, AUC, KS, and LIFT indicators can be used instead of AIC and BIC indicators. For some businesses, AUC and KS are indicators that are more suitable for business scenarios. For example, in the sorting business, the model built using the KS indicator has the advantage of using fewer variables but the KS of the model does not decrease on multiple test sets according to past experience.
2. When performing stepwise variable selection, use other data sets to calculate model evaluation indicators instead of using the modeling data set. Especially when the amount of data is large and there is a validation set in addition to the training set and test set, it is recommended to use the validation set to calculate evaluation indicators to guide variable selection. This helps reduce overfitting.
3. Support the use of partial data to calculate model evaluation indicators to guide variable selection. Scenario example: If the business needs to maintain a certain pass rate of N%, then the bad event rate of the first N% samples can be minimized, and all samples do not need to participate in the calculation. According to past experience: In appropriate scenarios, using partial data as evaluation indicators to select fewer variables than using all data, but the indicator that users are concerned about does not decrease in multiple test sets. Because the model only focuses on sample points that are easier to distinguish at the head, business goals can be achieved without too many variables.
4. Supports setting multiple conditions. Variables must meet all conditions at the same time before they can be included in the model. Built-in conditions include: P-Value, VIF, correlation coefficient, coefficient sign.
5. Supports specifying variables that must be entered into the model. If the specified variables to be entered into the model conflict with the conditions in 4, a complete mechanism is designed to solve the problem.
6. The modeling process is output to EXCEL, recording the reasons for deleting each variable and the process information of each round of stepwise regression.
7. When the number of configured CPU cores is greater than 1, multi-process parallel computing stepwise regression is automatically started.
In most cases, users do not need to interact directly with the Reg_Step_Wise_MP component. However, because ScoreConflow is a pluggable component, advanced users can use the Reg_Step_Wise_MP module separately like any other python module.
##### 4. Cutter

Perform equal frequency segmentation or segmentation according to specified split points, which has the following enhancements over the built-in segmenter in Python:
1. Mathematically provable analytical solution with minimum global error.
2. All split points come from the original values.
3. More humane support for left closed and right open: The last group is right closed. The minimum and maximum values of each interval come from the original data, which is different from the built-in splitter in Python, which changes the extreme values at both ends of each group.
4. The globally optimal segmentation solution can also be given for extremely tilted data.
5.Support weighted series.
6. Supports special values specified by users. Special values are grouped separately, and users can also configure multiple special values to be combined into one group.
7. Special values do not include null values, but if there are null values in the sequence, the null values will be automatically processed into a group.
8. Use the specified split point to cut the sequence. When the maximum or minimum value of the sequence exceeds the split point boundary, the maximum and minimum values of the split point will be automatically extended.
It is recommended to try to replace Python's built-in equal frequency segmentation component with Cutter.

##### 5.Filter

1. Six built-in filters: single value ratio filter, IV filter, IV variation filter, correlation coefficient filter, PSI filter, missing value filter.
2. The results and intermediate data will be saved in Excel and integrated in the model report.
3. Supports user-defined filters. Users only need to implement the filtering method. ScoreConflow will automatically integrate the results and intermediate data into the model report according to the interface specifications.
4. Single value proportion filter, IV filter, and missing value filter support pre-filtering.
5. Support users to specify the data sets involved in filter calculation.
6. Users can specify variables to delete or retain.

#### Recruitment Plan
ScoreConflow hopes to create the world's easiest-to-use, most comprehensive, and most effective scoring card model algorithm. This goal requires the participation of insightful people.
If you have a good idea that can enhance ScoreConflow and can realize it, in order to thank you for your contribution, the ScoreConflow organization will reward you with N% of the sales amount for each copy sold. The size of N is determined by the practicality of the idea and the difficulty of implementation.
If the algorithm you contributed needs to be protected, ScoreConflow has a complete set of self-developed algorithm protection systems to protect your rights.

In addition, if you can share your experience and skills in using ScoreConflow on the Internet, the ScoreConflow organization will refund the fees you paid that year.

#### WeChat consultation
WeChat ID: SCF_04
