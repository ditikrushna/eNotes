---
layout: post
title: "Machine Learning by University of Washington"
categories: misc
author: "Ditikrushna Giri"
---


##### Course Name : Machine-Learning Foundations A Case Study Approach 

#### Week1 :[Introduction] [PPT](https://d396qusza40orc.cloudfront.net/phoenixassets/ml-foundations/intro.pdf)

The Machine Learning Pipeline 

> Data -> ML Method -> Intelligence 

**Case Study Approach** 
Use various ML Methods in different case studies :
1. Regression Case Study 1: Predicting House Prices
2. Classifcation Case Study 2: Sentiment Analysis
3. Clustering Case Study 3: Document Retrieval
4. Matrix Factorization Case Study 4: Product Recommendation
5. Deep Learning Cases Study 5: Visual Product Recommender

**Overview** 
Week2 Regression 

Case Study: Prediction house prices
 - Models
	 - linear regression
	 - Regularization: Ridge (L2), Lasso (L1)
- Algorithms
    - Gradient descent
   -  Coordinate descent
- Concepts
    - Loss functions
    - Bias-variance tradeoff
    - Cross-validation
    - Sparsity
    - Overfitting
    - Model selection

Week3 Classification 
Case study: Analyzing sentiment

 - Models:
	- Linear classifiers (logistic regression, SVMs, perceptron)
    - Kernels
    - Decision trees
- Algorithms
    - Stochastic gradient descent
    - Boosting
- Concepts
    - Decision boundaries
    - MLE ensemble methods
    - Random forests
    - CART
    - Online learning

Week 4 Clustering & Retrival 
Case study: Finding documents

 - Models
    - Nearest neighbors
    - Clustering, mixtures of Gaussians
    - Latent Dirichlet allocation (LDA)
- Algorithms
    - KD-trees, locality-sensitive hashing (LSH)
    - K-means
    - Expectation-maximization (EM)
- Concepts
   - Distance metrics
    - Approximation algorithms
    - Hashing
    - Sampling algorithms
    - Scaling up with map-reduce

Week 5 Matrix Factorization & Dimensionality Reduction

Case study: Recommending Products

 - Models:
    - Collaborative filtering
    - Matrix factorization
    - PCA
- Algorithms
    - Coordinate descent
    - Eigen decomposition
    - SVD Algorithms
- Concepts
    - Matrix completion
    - Eigenvalues
    - Random projections
    - Cold-start problem
    - Diversity
    - Scaling up

Week 6 Capstone: An intelligent application using deep learning

**Getting Started with SFrame :** 
> Machine Learning Library scikit-learn 
> Data minipulation tool Pandas 
Tools above require a learning curve . This course uses GraphLab create that includes SFrame. 

    # Load a tabular data set 
    data = gaphlab.SFrame('people-example.csv')
    # View end of the table 
    data.tail() 
    #visulize any data structure in GraphLab Create 
    data.show() 
    # Categorical View 
    data['age'].show(view='Categorical') 
    # Some Simple Columns Operations 
    data['age].mean()
    data['age'].max() 
    # Create new columns in SFrame 
    data['Full Name'] = data['First Name] + ' ' +data['Last Name' ] 
	# use the appy function to do a advance trasnformations of our data 

	def transform_country(country):
	      if country == 'USA':
	     return 'United States'
	     else:
	      return country
	  transform_country('USA')
	   
	  data['Country'].apply(transform_country)

#### Week2 :[Regression: Predicting House Prices] [PPT](https://d396qusza40orc.cloudfront.net/phoenixassets/ml-foundations/regression-intro-annotated.pdf)

### Week 3 : Classification:[PPT](https://d396qusza40orc.cloudfront.net/phoenixassets/ml-foundations/classification-annotated.pdf) 

 -  **Clasification Modeling** Analyzing the Sentiment of Reviews 
***Understand aspects of restaurant review***
	- build a restaurant review app
	-	categories for review e.g. experience, ramen, sushi
	-	Break all reviews into sentences in a Sentence Sentiment Classifier
	-	Average the predictions
	-	Display the most positive or negative reviews 
- **Classification Aplications**
> Input (sentence) -> Classifier -> Output (predicted rating)

- **Examples**
	- Webpage classification by category e.g. education, finance, technology
	- Spam filtering: checks sender, text, ipaddress, etc
	-	Image classification
	-	Personalized medical diagnosis
	-	Reading your mind by [FMRI](https://g.co/kgs/Dag4BT)

- **Simple Threshold Classifier**
	-	list of +ve words: great, awesome, etc
	-	list of -ve words: bad, terrible, etc
	-	if # +ve words > # -ve words => ŷ = +ve else ŷ = -ve
		Ex. "Great sushi, awesome food, but terrible service" => +2, -1

- **Problems with Threshold Classifier**
	-	Populating initial +ve and -ve word lists
	-	Words have degrees of sentiment: e.g. "great" > "good"
	-	Single words are not enough: "good" vs "not good"
- The first two can be address by learning a classifier.The 3rd issue can be address by more elaborate features Word Weight great 1.5 awesome 1.2 bad -1.0 terrible -2.1 awful -3.3 restaurant, the, we, where, ... 0.0
e.g. "Sushi was great, the food was awesome, but the service was terrible"

- **Decision Boundaries**
	- For linear classifiers
		- When 2 weights are non-zero: **line**
		- When 3 weights are non-zero: **plane**
		- When 2 weights are non-zero: **hyperplane** 
- **Evaluating Classification Models Training and Evaluating a Classifier**
	> ***Training a classifier = Learning the weights**
		
	- Split data into training and test sets
	- Training set is passed to learned classifier to learn weights of words
	-	Test set is evaluated by error & accuracy
	
	- ***Test example "Sushi was great"*** 
		- Feed the sentence ^ to the learned classifier
predict ŷ is +ve
		- Pass multiple test cases and compare correct vs mistakes
	- ***Classification error & accuracy***
		- Error = (# mistakes) / (total # sentences)
		- Best possible value = 0.0 
		-  Accuracy = (# correct) / (total # sentences)
		- Best possible value = 1.0 
		- Error = 1 - accuracy 
	- What's a good accuracy?
		- Purely random guessing on a binary classification = 0.5 accuracy
		- For k classes, accuracy = 1/k
		- we should at least beat random guessing
This can be counterintuitive e.g. 

	> 	"90% email is spam" if we predict 100% email is spam we get 90%  accuracy
		
	- ***Questions to ask:***
		- Is there class imbalance?
		- How does it compare to a simple, baseline approach?
    Random guessing
    Majority class
		- Most importantly: what accuracy does my application need?
		- What is good enough for my users experience?
	        - What is the impact of the mistakes we make?



