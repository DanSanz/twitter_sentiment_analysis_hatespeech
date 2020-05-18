
# Twitter sentiment analysis to detect hate speech
<p align="center">
  <img src="https://github.com/matteomm/twitter_sentiment_analysis_hatespeech/blob/master/figures/cover.jpg" width=750>
</p>


Different tweets from two sources were grouped in order to build a larger collection of roughly 40000 tweets contaning positive, neutral and offensive language. Offensive language is also divided into simple offensive language and hate speech.
Hate speech's definition is taken from Cambridge Dictionary: "public speech that expresses hate or encourages violence towards a person or group based on something such as race, religion, sex, or sexual orientation". The main goal of this project is to build a model capable of identifying hate speech on Twitter. In the final section winning model runs across fresh tweets collected daily from Twitter API in the UK, showing percentage of overall tweets labelled as offensive language or hate speech.

Promptly identifying hate speech and overall offensive language is a very important concern for all major social media platforms. According to the public order act from 1986, any communication which is threatening or abusive, and is intended to harass, alarm, or distress someone is forbidden. The penalties for hate speech include fines, imprisonment, or both. It is very important to ensure social platform media only act as a medium of spreading free speech and constructive ideas. One of the main challenges when it comes to hate speech detection is also to differentiate it from any other type of offensive language.

The final dashboard showcasing percentage of language tone on Twitter can be found here on Heroku. Fresh tweets are pulled every 24 hours.

Contacts:
* [e-mail](matteotortella4@gmail.com)
* [Linkedin](https://www.linkedin.com/in/matteo-tortella-0a4274130/)




### Executive Summary

Start with one or two sentences here that contextualises what your project matters here.
These two sentences will demonstrate your business understanding. 

Next, in a second paragraph, write how you were able to make a data science operationalization of the problem.
For example, you might say that in order to help solve this problem you set out to build a classification ML model in order to automate some process. 

Third, you then write what you did on the project that is a bit more technical.
Here you might say that you took data from [here and make it a link to the original data]() and then ran `a list of models you ran here` in your analysis.
Then end with one sentence that picks what your best model was and how it performed.

Lastly, you say in one or two sentences why this matters. 
For example, now as opposed to before this data analysis, you can now predict X better than Y. 

The goal of this project was to create a `regression/classification` model that was able to predict `what you set out to do`.

> If you are able to swap out the text here with what your case example is you will demonstrate the following:
> 1. You get why what you're doing 'matters'
> 2. You are able to take ill defined problems and turn them into something a data scienst can solve
> 3. You show off your analystical and modeling chops.
> 4. You are able to communicate technical things you do.

# Table of Contents

1. [ File Descriptions ](#file_description)
2. [ Technologies Used ](#technologies_used)
3. [ Executive Summary ](#executive_summary)
    * [ Data Cleaning and Feature Engineering ](#datacleaning)
    * [ Exploratory Data Analysis ](#eda)
    * [ Modelling ](#modelling)
    * [ Twitter API and MySQL Storage ](#twitterapi)
    * [ Model Evaluation and Dashboard ](#insights)
  


<a name="file_description"></a>
## File Descriptions
- .ipynb_checkpoints: different notebooks version going from preprocessing to modelling
-  notebooks: contains all the different notebooks used throughout the project from data cleaning to final app
-  data: contains dataset used for the analysis both processed and raw
-  references: links to the source material referenced in the notebook
-  images: jpg images taken from the jupyter notebook
-  twitter_presentation: pdf format of a presentation with key insights for non-tecnhical stakeholders

<a name="technologies_used"></a>
## Technologies used
- Python
- Pandas
- Keras
- Nltk
- Tweepy
- MySQL
- Seaborn
- Matplotlib
- Streamlit
- Heroku

<a name="executive_summary"></a>
## Executive Summary

Cyber bullying and aggressive language on social plaforms are one of the plagues of our modern time. Freedom of speech online can easily derail into offensive, unjustified and unconstuctive criticism towards sexual, political and religious beliefs.
ML classifiers and the wealth of data available on these platforms offer a valid solution in order to mitigate this issue.

In this project, a series of classifiers such as Logistic Regression, Decision Trees and CNN were trained on 40000 thousand tweets human labelled as offensive and not offensive. The 40000 tweets were assembled by combining two different sets. One of them was originally taken from an [Analytics Vidhaya](https://datahack.analyticsvidhya.com/contest/practice-problem-twitter-sentiment-analysis/) competition while the second dataset was a collection of 20000 offensive tweets found on [Github](https://github.com/t-davidson/hate-speech-and-offensive-language/tree/master/data).

After the initial preprocessing, the first section is focused on training a classifier at recognising hate speech. Our final winning model was Logistic Regression with a final accuracy score of xyz.

The second section concentrates more on using the refined model to make predictions on unseen Tweets freshly taken from the Twitter API and showcasing out findings on a web app deployed on Heroku.


<a name="datacleaning"></a>
## Data Cleaning and Feature Engineering

As mentioned above the initial dataset was designed through the combination of two distinct sets from the web. The raw initial dataset was designed to have no class imbalance as we have selected exactly 21421 positive and 20610 negative tweets. Given the balanced nature of the training set, this project will mainly look at accuracy and f1 score as success metrics. 

Cleaning was performed with a some iterations of regex syntax to get rid of re-tweets, handles and special characters. Duplicate tweets were also removed and lemmatization with part of speech was also applied to all tweets. The last stage involved removing stopwords and also words shorter than three characters as they do not usually carry very valuable meaning. However, stopwords such as 'but' and 'not' were kept for neural networks sequencing. We created two additional columns, 'tweet_length' and 'handle_count' to investigate whether these two factors have any impact on positive/negative language.

<a name="eda"></a>
## Exploratory Data Analysis

The EDA section provided some useful insights into the very fabric of the words used in these tweets. Wordclouds were created to showcase the most common 1,2 and 3-grams present in the text. Attaching below a comparison between positive and negative lexicon, larger words correspond to higher frequency.

<p align="center">
  <img src="https://github.com/matteomm/twitter_sentiment_analysis_hatespeech/blob/master/figures/word_clouds.png" width=750>
</p>

Also, distributions of lengths between positive and negative tweets was also analysed and, as shown in the graph below, negative tweets seem to be on average shorter than their positive counterpart. 1 represents negative tweets while 0 positive ones. It is possible to see that most of the negative tweets are concentrated on the left side of the graph corresponding to shorter lengths. A simple t-test confirmed that the mean difference is significant with p-value smaller than 0.001.

<p align="center">
  <img src="https://github.com/matteomm/twitter_sentiment_analysis_hatespeech/blob/master/figures/length.png" width=750>
</p>

In the last section, the relationship between number of handles and aggressiveness was measured by plotting again number of positive/negative against overall number of handles. The vast majority of the tweets had somewhere in between 0 and 3 handles with a stark difference between 0 and 1 handles tweets, the latter having a significantly higher proportion of offensive tweets along with the 2 and 3 class. This could be explained by people directed their rant at someone through the use of handles.

<p align="center">
  <img src="https://github.com/matteomm/twitter_sentiment_analysis_hatespeech/blob/master/figures/handles.png" width=750>
</p>

Are aggressive people less verbose? Add final graph

<a name="modelling"></a>
## Modelling
