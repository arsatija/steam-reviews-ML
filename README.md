# Steam Reviews Prediction

## Project setup

Install python with the following packages from the `/requirements.txt`

## Business Understanding
The objective of the notebook is to be able to predict whether or not a game will be recommended based off the review. By analyzing reviews, the model identifies key words and phrases that lead to positive or negative recommendations. This can help game developers and marketers understand what aspects of a game are most appreciated by users when creating a sequel or a game in a specific genre.

## Data Understanding

The data we will be looking at is a dataset acquired from Kaggle containing Steam reviews from 2017 and before.
> https://www.kaggle.com/datasets/andrewmvd/steam-reviews

The data will be downloaded and placed in the following path with the following name: 
    
    `/data/dataset.csv` 
    
It should be about a 2.6 gb file when unzipped.
A sneak peek of the data:

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>app_id</th>
      <th>app_name</th>
      <th>review_text</th>
      <th>review_score</th>
      <th>review_votes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10</td>
      <td>Counter-Strike</td>
      <td>Ruined my life.</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10</td>
      <td>Counter-Strike</td>
      <td>This will be more of a ''my experience with th...</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10</td>
      <td>Counter-Strike</td>
      <td>This game saved my virginity.</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10</td>
      <td>Counter-Strike</td>
      <td>• Do you like original games? • Do you like ga...</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10</td>
      <td>Counter-Strike</td>
      <td>Easy to learn, hard to master.</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>

We can see that the data has over 6 million rows with the following structure:
1. `app_id`
   * Game ID
2. `app_name`
   * Game Name
3. `review_text`
   * Review Content
4. `review_score`
   * 1 for recommended, -1 for not recommended
5. `review_votes`
   * number of votes for how helpful the review was

The rows that will be relevant for training the model will be `review_score` and `review_votes` as we just need the content of the review and whether or not it was a positive review.

## Data Preparation
We need to remove the duplicate and NA rows which cuts the data down about 2 million entries. Once complete, we are going to be looking at only the two aforementioned rows in a 5% sample size. This sample size can be adjusted to affect accuracy of the model but also time complexity of the model. We settled with 5% for now to keep the model at a reasonable train time on a local machine. The next step would be to run the train test split with a 20% test size from that data. Next we will vectorize the data using the `TFID Vectorizer` from `scikit-learn` removing english stopwords and looking at unigrams to trigrams.

## Modeling
For this project we are going to create 3 models.
1. **Baseline Model:** Dummy Classifier Model
2. **First Model:** Decision Tree Classifier
3. **Improved Model:** Random Forest Classifier 

We will create a baseline model that should not be very good just to have a baseline to start comparing the other models to. We then start with a Decision Tree model with an okay performance that can definitely be improved with hypertuning with a GridSearch. However, upon further research I found that a Random Forest model may be better for this use case and it in fact was with the base parameters. We can further fine tune the Random Forest Classifier , given more time, by feeding it more data or messing with hyperparameters for this model as well.

## Evaluation
I stored the precision and recall scores of each model in a dataframe to then represent in the following bar graph to help conclude which model performed the best. It was evidently the "Improved Model" of the **Random Forest Classifier**.
![alt text](/img/image.png)

We can look at the confusion matrix for this model to get a better understanding of the precision of the model. ![alt text](/img/image-1.png)
We can see a lot of overfitting however, this is much preferred to underfitting data in a situation like this. The crux of this project is to determine features that contribute to positive reviews rather than focusing on the negative features. There were almost no false positives which is really good for our intentions of using the model.

The purpose of this project is to find features that contribute to positive reviews, so let's look at the most important features as deemed by the model:
![alt text](/img/image-2.png)
We can see that not many phrases were recognized as important features but it's likely due to the small sample of data that was fed through the model. Additionally, we can see arguable stop words also contributing to the importance such as 'just'. This is something to look out for in the future as the model should still be further trained with hyperparameters in effect and more training data being sent through.

I want to emphasize that the beauty in this project is not necessarily the model predicting yay or nay but in the features that can be identified as important for either direction. Game developers can look at this newly organized data when pursuing the creation of a new game to find what is something that is sought after in games of a specific name or genre.

Although the model was mostly successful in predicting yay or nay, we want to further reduce the false positives that are returned by the model. However, it is worth noting that the current behavior is preferred to underfitting due to the users of this model wanting to further focus on what is positive and good for a game rather than the negative because by doing what is desired you avoid what is undesired.

### Next Steps:

The model can always be further improved but the real next steps to be accomplished before deployment is further honing in on the features that contribute to positive reviews and categorizing them for specific game franchises or genres to a centralized location that can quickly be parsed for the information a game developer or studio is looking for. In order to improve the model's accuracy or increase the list of important features, we can increase the sample size that was fed into the model (for time purposes) and enforce a more equal weighted distributions between the samples that are picked between positive and negative sentiments.

**Steps**: 
1. Improve the model
2. Further filter important features
3. Create associations between the important features and the sentiment
4. Store categorized features in a database that is accessible through a webapp.
5. Profit