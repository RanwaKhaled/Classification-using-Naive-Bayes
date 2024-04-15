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
