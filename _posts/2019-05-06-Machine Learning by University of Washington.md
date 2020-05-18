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
