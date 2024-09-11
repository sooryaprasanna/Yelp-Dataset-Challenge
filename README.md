<img width="400" alt="image" src="https://github.com/user-attachments/assets/44357316-c756-4c4e-9dc1-de138db65db9">

**Sentiment Analysis and Recommendation Model**

- Implemented topic models using sentiment analysis to predict the review star rating and built recommendation model using Mahout’s ALS algorithm to improve suggestions with 87.4% accuracy.

Skills : Hadoop Map Reduce, Apache Spark, Apache Pig, Java

**Background**
- Most of the reviews are skewed towards higher ratings range from 3.0 to 4.0 stars, with very few below or above.
- Ratings are subjective and is difficult for new customers to gauge service satisfaction.
- Decided to go with a granular classification of sentiment to predict exact rating stars.

**Ideation**
- Goal is to build an accurate model by analyzing the sentiment of the user reviews. 
- Predict a star rating based on the sentiment.
- The calculated predicted rating is sent to the recommendation model.
- Mahout's ALS algorithm (Machine Learning) to recommend and predict the business that the user may like.

**Dataset**
- Yelp offers open source dataset, which includes the data of 55,245 businesses, 552,979 users and 2,225,864 reviews. 
- This 2.5G dataset contains information about the businesses owned, reviews written and users using the service, their ratings to businesses.

**Prediction Strategy**
- Divide the review text into key-value pairs, with key being the word and the value being the word count.
- Join the review words with the positive and negative word dictionary.
- Taking its neighbors into consideration to calculate the ratings. The sentence "Food is not bad" is not a poor review, we handled them as well (neighbors technique).

**Formula**
- 2.5 + [(Positive + Negative) * 2.5 / (Positive + Negative)]

**Data Flow**

<img width="600" alt="image" src="https://github.com/user-attachments/assets/56a0b5f0-c549-4074-8bb0-84e5540e8b29">

**Result**
- The 'difference' specifies the contrast between the actual and predicted ratings.
- Considering the neighbors in Spark, 900 of every 1000 reviews differ with the actual rating by <=1.
- The numbers reduce substantial for large differences 2 and 3.
- Spark gives a precise result in contrast with Map Reduce and Pig as their neighbors are not considered.

**Recommendation Strategy**
- The predicted ratings are divided into training (80%) and test set (20%).
- Since ALS does not work with alpha-numeric IDs', we map them to uniquely generated numeric IDs to produce a modified training and test dataset.
- The training set is fed to the Mahout's Alternating Least Squares (ALS) algorithm from the Scala Machine Learning library.
- Generate the recommendation for each ID and remap the numeric IDs to alpha-numeric IDs.
- Calculate the Mean Square Error (MSE) for the predicted rating.

**Result**
- We calculate the recommendation for all users. Top 3 samples below :
  - Rating (8861, 1498, 4.997003739462084)
  - Rating (8861, 953, 4.928069290238446)
  - Rating (8861, 2955, 4.871139293965359)
- The mean square error and accuracy are computed for gauging the accuracy of our recommendation model.
- Mean Square Error : 0.041
- Accuracy of our model : 87.4%

