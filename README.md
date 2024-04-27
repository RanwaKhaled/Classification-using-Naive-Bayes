## `Name` Ranwa Khaled Fathy Metwally, `ID` 2203153
# Classification-using-Naive-Bayes
In this notebook the **Naive Bayes** algorithm was used to predict the income of some people, in 2 classes:
* *<=50K*
* *>50K*
Based on the following features:
* Age
* Workclass
* Fnlwgt
* Education
* Education num
* marital status
* Occupation
* Relationship
* race
* sex
* capital gain
* capital loss
* hours per week
* Country
## To apply the Naive Bayes algorithm a few methods were created 
### Methods to calculate likelihoods 
#### 1- Numerical Features
`calculate_numerical_likelihood` 
takes the value for the sample along with the whole column of the feature & the target label of the sample along with the target column <br>
**Returns:** The likelihood of the sample using this formula:<br>
<img src="https://github.com/RanwaKhaled/Classification-using-Naive-Bayes/assets/77844198/26e58a54-56f4-4c12-85fb-f43edd32f24d" width = 400>
<br>*The method is to be called with each value in the sample*
#### 2- Categorical Features
`likelihood_dict`
creates a dictionary of the likelihood for each value of the categorical features<br>
*The method is to be called at the beginning before entering any loops* <br>
**Returns:** The likelihoods dictionary for the categorical features <br>
<img src="https://github.com/RanwaKhaled/Classification-using-Naive-Bayes/assets/77844198/04d58b04-be24-48b6-b45c-0825ebd92d61" width = 400>
<br>
The method uses another method inside which is `calculate_likelihood`
This method calculates the conditional probability of each value for each feature given it belongs to a certain class and it is used to calculate the value that will be inserted in the dictionary<br>
**Returns:** The conditional probability for the value given it is in a certain class
### Method to calculate the prior probability for each label in the target column
`calculate_prior_probs`
The method returns an array of prior probabilities, one for each label, using this formula: <br>
*number of instances the label occurs / the number of samples*
### Applying the Naive Bayes algorithm 
`naive_bayes` method which takes as parameters:
* The dataset: pandas data frame
* The set of features we will use to make the prediction: pandas data frame
* The target labels: array-like sequence <br>
#### Before entering any loops the method starts by calculating: 
*The prior probabilities for each label* - using the method `calculate_prior_probs` <br>
*Calculating the likelihood dictionary for the categorical features* - using the method `likelihood_dict` <br>
<img src="https://github.com/RanwaKhaled/Classification-using-Naive-Bayes/assets/77844198/fa0f13e2-fb7e-4358-9adf-5124cddaf6d8" width=400>
#### Iterating over each sample in the dataset 
To calculate the likelihood for each class we go over each feature and calculate the likelihood for that feature belonging to the class and multiply all of them together to store in an array of likelihoods each value representing the **Π of the conditional probabilities for all features given they belong to a certain class** <br>
<img src="https://github.com/RanwaKhaled/Classification-using-Naive-Bayes/assets/77844198/3119e799-a276-42eb-9120-17be59d28798" width=400>
<br>
Calculating the **posterior probability** for each sample: <br>
We multiply the likelihood for each class by the prior probability 
and then we store the prediction in an array where the prediction is the index of the highest posterior probability **0 if the posterior prob of the first class is bigger** and **1 if the posterior prob of the second class is bigger**
**The method then returns:** an array of predictions, 1 for each sample
![image](https://github.com/RanwaKhaled/Classification-using-Naive-Bayes/assets/77844198/bb6e0933-c090-4bca-a1c6-0e47342f2dce)
<br><br>
## Driver Code
**Dataset used:** the `adult_test.csv` containing *16 281* sample <br>
First, we separate the target columns from the feature columns 
we use the `naive_bayes` method and store the array of predictions in a variable called *y_pred* <br>
`# make the prediction` <br> 
`y_pred = naive_bayes(dataset, features, target)`
### Evaluating the model 
To create a confusion matrix we use the `confusion_matrix` class found in the sklearn library, and the results are as follows:<br> 
<img src="https://github.com/RanwaKhaled/Classification-using-Naive-Bayes/assets/77844198/93aa4e9e-211b-400b-a594-b06cc5ca4354" width = 400>
<br> We also see the plotted confusion matrix using matplotlib library: <br>
<img src="https://github.com/RanwaKhaled/Classification-using-Naive-Bayes/assets/77844198/c49bc73b-d9b1-49d4-a4ec-d10d04fdb03d" width=400>
### Sensitivity and Specificity 
Finally, we calculate the sensitivity and specificity of the model using the formulas:<br>
<img src="https://github.com/RanwaKhaled/Classification-using-Naive-Bayes/assets/77844198/18e6e4af-362a-44fa-9c12-e56628eb4eb4" width=400>
<br>
and get the following results: <br>
<img src="https://github.com/RanwaKhaled/Classification-using-Naive-Bayes/assets/77844198/3258babd-1f05-42b3-b1c3-a8e7f15959fd" width=500>
<br>
According to the article:<br>
Power M, Fell G, Wright MPrinciples for high-quality, high-value testingBMJ Evidence-Based Medicine 2013;18:5-10.<br>
For a test to be useful, sensitivity+specificity should be at least 1.5 (halfway between 1, which is useless, and 2, which is perfect). <br>
Thus we find that the sum of the sensitivity and specificity values produced is around **1.546**.
