# Steam Reviews Prediction

## Business Understanding
The objective of the notebook is to be able to predict whether or not a game will be recommended based off the review. By analyzing reviews, the model identifies key words and phrases that lead to positive or negative recommendations. This can help game developers and marketers understand what aspects of a game are most appreciated by users when creating a sequel or a game in a specific genre.

## Data Understanding

The data we will be looking at is a dataset acquired from Kaggle containing Steam reviews from 2017 and before.
> https://www.kaggle.com/datasets/andrewmvd/steam-reviews

The data will be downloaded and placed in the following path with the following name: `/data/dataset.csv`. It should be about a 2.6 gb file when unzipped.
A sneak peek of the data:

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
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