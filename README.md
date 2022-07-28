# Animal-Recognition-Image-Processing
This web app recognizes animals from their images using machine learning

* Created a tool that recognizes an animal(>80% precision) when a user imports an image into it. 
* This helps wildlife industries recognize animals for various purposes(research, studies...).
* Used over 1500 animal images as base for this model.
* It transforms the image input(whatever the dimensions) as grayscale, then hog transformation and outputs probabilities of the animal in the picture.
* Optimized svm, knn, sgd and logistic regression, even verifying learning curves to reach the best model.
* Built a client facing API using flask. 
* Import an image. Get the animal in it. [Try it !!!](https://animal-image-processing.herokuapp.com/)


## Code and Resources Used 
**Python Version:** 3.10  
**Packages:** pandas, numpy, scikit-learn, scikit-image, scipy, flask, pickle, matplotlib, os, re, glob          
**For Web Framework Requirements:**  ```pip install -r requirements.txt```   
**Heroku Productionization:** https://animal-image-processing.herokuapp.com/

## Animal Types
The following animals were in the data:
* 'bear', 'cat', 'chicken', 'cow', 
* 'deer', 'dog', 'duck', 'eagle',
* 'elephant', 'human', 'lion', 'monkey', 
* 'mouse', 'natural', 'panda', 'pigeon',
* 'rabbit', 'sheep', 'tiger', 'wolf'.

## Finding the data | Transforming it
I created paths towards the different image files and got them in an array.
Then, I applied the following transformations on the image array:
* Converted it grayscale
* Resized and rescaled appropriately
* Used a hog transformer to transform it into a format the model can understand
* Resized and rescaled appropriately
* Standardized the array
* Fit into the model

## Model Building 

I tried four different models and evaluated them using cohen kappa score. I chose MAE because it is relatively easy to interpret and particularly suited for image recognition scores.   
Furthermore, to ensure the models are not overfitting, I plotted their learning curves for test and train data and spotted immediately which ones were bad.

Why I chose these four different models:
*	**Stochastic gradient descent** – Since the data is unconstrained.
*	**Logistic Regression** – I thought there it could detect a logical pattern between animal's shape after being hog transformed for example.
*	**KNeighborsClassifier** – Again, since it groups neighbours, it could be suitable for grouping the hog transformed area and find patterns.
*	**Support Vector Machine** – Since there may be outliers(like different animals having the same shape), I thought svm could capture that.

## Model performance
The svm model outperformed the other approaches on the test and validation sets and did not overfit.
*	**Support Vector Machine** : CKS = 82.05%
*	**Logistic Regression**: CKS = 77.43%
*	**KNeighborsClassifier**: CKS = 62.61%
*	**Stochastic gradient descent**: CKS = 56.4%                
CKS = Cohen Kappa Score. >50% is usually good.

## Productionization 
In this step, I built a flask API endpoint that was hosted on heroku. The API webpage takes in a photo of an animal and outputs the animal that is in the photo. 
