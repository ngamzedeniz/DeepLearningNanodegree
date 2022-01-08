# Data: graduate school admissions data (found at http://www.ats.ucla.edu/stat/data/binary.csv) 
This dataset contains three input features: GRE score, GPA, and undergraduate school rank (numbered 1 through 4).
Institutions with a rank of one have the highest prestige, while those with a rank of four have the lowest.

The goal is to predict whether a student will be admitted to a graduate program based on these characteristics. 
We'll use a network with one output layer and one unit for this. For output unit activation, we'll use a sigmoid function.

# Cleanup of data
You might think there will be three input units, but the data must first be transformed. 
The rank feature is categorical, and the numbers do not encode any relative values. 
Rank 2 does not cost twice as much as rank 1, and rank 3 does not cost 1.5 times as much as rank 2. 
Instead, we must encode rank using dummy variables, dividing the data into four new columns encoded with ones or zeros. 

Rows with rank 1 have a value of one in the rank 1 dummy column and a value of zero in all other columns. 
Rows with rank 2 have a single value in the rank 2 dummy column and zeros in all other columns. And so forth.
This can be found in the file dataprep.py

We'll also need to standardize the GRE and GPA data, which means scaling the values so that they have a mean of zero and a one-standard-deviation standard deviation. 
This is required because the sigmoid function squashes both very small and very large inputs.
Because the gradient of extremely small and large inputs is zero, the gradient descent step will also be zero. 
Because the GRE and GPA values are fairly large, we must be extremely cautious about how we initialize the weights.

You need to implement:

The network output: output.
The output error: error.
The error term: error_term.
Update the weight step: del_w +=.
Update the weights: weights +=.
