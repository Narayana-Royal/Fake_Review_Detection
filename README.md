# Fake Review Detection on Products using ML

## Detecting Fake reviews on Amazon
### Springer Research Paper Link : https://link.springer.com/chapter/10.1007/978-981-19-9304-6_54

## Table of Contents

1. Problem Statement
2. Dataset along with features .
3. Approach Used to solve the Problem
4. Explanation along with the Code 
5. Results with Screenshots

**1. PROBLEM STATEMENT**: 
> It's hard to exaggerate how crucial user reviews are in figuring out an organization's e-commerce income. Before purchasing any goods or service, online customers rely on produc REVIEWS . As a result, firms must consider how reliable internet reviews are because it might directly affect their reputation and bottom line. Because of this, some businesses pay spammers to post false reviews. These false reviews profit from consumer buying choices. So in order to detect these reviews there's a need to create a model which can predict the fake ones 

**2. DATASET**: 
> https://www.kaggle.com/datasets/lievgarcia/amazon-reviews

> Also dataset csv file is uploaded in this github repository.

> Features: DOC_ID, RATING, VERIFIED_PURCHASE, PRODUCT_CATEGORY, PRODUCT_ID, PRODUCT_TITLE, REVIEW_TITLE, REVIEW_TEXT, LABEL.

**3. APPROACH USED to solve the Problem**: 

* *As our problem statement shows that we have to create a model to predict the fake reviews .The following steps are done to achieve this.*

**MAIN APPROACH:**
> My Approach for detecting the fake ones are like whenever in the review text, if there are more number of verbs than nouns in review text then the review will most likely to be fake and if there are more number of nouns than verbs in review text then it is a genuine one.

> This approach was even given by cornell university researchers and concluded how to detect fake ones

> Here's the link of researcher conclusion: https://reputation.com/resources/articles/spot-fake-reviews-how-to/#Look

> <img width="966" alt="Screenshot 2023-07-25 at 6 31 16 PM" src="https://github.com/Narayana-Royal/Fake_Review/assets/88378136/d706c6b8-321c-4693-ba6a-5fd1740e19c4">


**IN-DEPTH EXPLANATION OF THE APPROACH:**
> In order to consider the parts of speech of each word in the given review text, This can be done by a method called POS Tagging (Parts of speech tagging).

> Firstly, the review text will be tokenized as sequence of words by removing the unnecessary symbols and having only alphabets in each word. Later in order to reduce the number of words. We can use a method called stemming , this basically takes only one word among multiple set of words which conveys the same meaning. (For example: Discover , Discovering , Discovered all 3 conveys same meaning so we can reduce these 3 to 1 word by using stemming method).

> Secondly, Now our data is in sentence format after cleaning. So at first I split the sentence into words using nltk and perform POS Tagging (Parts of speech tagging) for each word, which basically assigns respective Parts of Speech for each word.

> So, considering only one review text, if there are more number of nouns than verbs for each word in a sentence. Then it is said to be real one. and if more verbs>nouns then it is fake. This will be the approach for any review text to classify it whether it is fake or real.




**4. Explanation along with the Code**:

*STEP 1 : DATA CLEANING*

> Importing the necessary libraries to perform dataset operations including saving built models using pickle, nltk for stopwords removal (i.e data cleaning) , regular expression for searching in data etc..

> Reading the amazon reviews dataset using PANDAS READ method.

> Performing Tokenization and Stemming. At first, To tokenize we need to remove the symbols and other unnecessary exclamations. This can be done by subtracting the unwanted things using regular expression and after removing we can now split the whole sentence into words. 

> Now we can remove the stopwords which are not useful for our machine learning model predictions. Also , to reduce the number of words I have done stemming which places only one word among multiple words which conveys the same meaning.(For example: Discover , Discovering , Discovered all 3 conveys same meaning so we can reduce these 3 to 1 word by using stemming method). Make a list of string into one string using join method. and append it to the corpus which has empty string. All these process is done for each review text.

*STEP 2 : DATA Processing*

> Taking the values of review text in this dataset as target variable "y".

> We already have target variable "y". Now Let's focus on what we need to do for X variable (i.e features).

> Now we have a corpus of review texts. This texted data can be converted to numerical form using count vectorizer. This count vectorizer form a list of unique words and assigns 1 when there is word present in that review and if it is not present it assigns 0. After performing the count vectorizer, now Storing the data of 0s and 1s in X variable. 

> Independent to X variable , Now in order to count the number of verbs and nouns in a sentence, which helps to predict the real/fake ones, I performed POS Tagging. This basically means, if there are more number of nouns than verbs then review text is true and if it's vice versa then its false. To convert it into machine readable form. I performed this, if the review text is True then the order will be of one kind (2d array with 1,0) and if its false then order will be of another (2d array with 0,1).

> Now append the above X variable data which has data after performing Count Vectorizer with the data after performing POS Tagging.
> So now X has data of all 0s and 1s after performing Count Vectorizer and POS Tagging.

> Also, In order to consider other categorical features like RATING, VERIFIED_PURCHASE and PRODUCT_CATEGORY. I converted those categirical values into numerical using Label Encoding which converts categorical values as numericals (starting from 1,2,3...). To convert these numericals into binary I have used OneHotEncoder which comverts into binary form (0s and 1s).
> So now X will be appended with the data that came after performing LabelEncoding and OneHotEncoder.

*STEP 3 : MODEL Building and Predictions*

> Now that we have X and y variables ready. I have split the dataset into training (80%) and testing dataset (20%).

> Building two different models for these dataset which are Bernoulli Naive Bayes (As our data is in Binary we can use BernoulliNB). Another one will be the SVM. Each model is fitted with the training data and ready to make the predictions using testing data. Overall, SVM gave better accuracy.

*STEP 4 : MODEL Building and Predictions*

> https://www.amazon.in/Microsoft-i5-1035G1-Touchscreen-Graphics-THH-00023/product-reviews/B08SX5XVBK?reviewerType=all_reviews




**5. Results with Screenshots**: 

> 1. Reading data

<img width="750" alt="Screenshot 2023-04-27 at 2 04 42 PM" src="https://user-images.githubusercontent.com/88378136/234806998-1fa8031a-4609-4972-9444-6fcfbf01fe15.png">

> 2. Changing categorical values to numerical

<img width="750" alt="Screenshot 2023-04-27 at 2 04 59 PM" src="https://user-images.githubusercontent.com/88378136/234807868-0b9abf87-10be-43f4-8c90-aeb4ec06dedb.png">

> 3. Filling the missing values

<img width="750" alt="Screenshot 2023-04-27 at 2 05 11 PM" src="https://user-images.githubusercontent.com/88378136/234808025-0c42e356-a47f-4306-b6d8-3f5ba35af585.png">

> 4. Visualising the graphs of cleaned data to extract insight

<img width="750" alt="Screenshot 2023-04-27 at 2 05 26 PM" src="https://user-images.githubusercontent.com/88378136/234808180-87388a88-acd7-49e7-b683-bdb2970cd157.png">

> 5. Finally!!! Feature scaling is done! (Now the data is ready to perform in training of the model)

<img width="750" alt="Screenshot 2023-04-27 at 2 05 41 PM" src="https://user-images.githubusercontent.com/88378136/234808228-eefaf084-9cb9-4759-a702-36a6a11fe9fa.png">


