# Anxiety-or-Depression
Classifying Social Media Posts between anxiety or depression

Classification of Reddit Posts Using NLP Modeling Techniques¶
Note: this project was prepared with four separate workbooks which should be read in sequential order:
'Data Acquisition (Book 1).ipynb'

This book represents steps taken to acquire the data necessary for this project and save the data as a csv file for use in this project
'Cleaning and EDA on Acquired Data (Book 2).ipynb'

This book takes the csv saved from Book 1, reads it in and is used to perform any necessary cleaning on the acquired data as well as explore the data prior to performing modeling. A new csv representing the cleaned data is the output of this file.
'Modeling (Book 3).ipynb'

This book reads in the cleaned csv from Book 2 and is used to create 4 NLP models to prepare the analysis
'Additional models (Book 4).ipynb'
THis book contains additional models that I prepared as part of this project that were completed, but did not yield as valuable results as those in book 3 and were not used for presentation purposes. Goal of this book is to maintain an appendix of the body of work
Executive Summary:
For this project, I used the PushShift API to extract posts from two similar but distinct sub-reddits and create various Natural Language Processing(NLP) models to build, train and test a classification model for the acquired posts and determine whether the model can classify the posts appropriately.

These two sub-reddits were selected to evaluate whether models could be built that effectively classifies posts when there is overlap between the content.

My research (and personal experience) has revealed that depression and anxiety are overlapping but distinct conditions. If an effective model can be built to classify text data as belonging to a 'depression' class or an 'anxiety' class, there are myriad applications beyond data science. For example, medical professions could use a model to evaluate patient writing as part of a diagnostic assessment. Or in severe cases, websites such as reddit could use the model to potentially identify a user exhibiting severe symptoms in their writing and push a banner advertisement with intervention resources aimed at helping a user in distress.

This project was born out of the problem of how to classify posts with potentially overlapping information. According to the Mayo Clinic, depression and anxiety are unique conditions that commonly occur together and have similar treatments. For example, anxiety may occur as a symptom of major depression and depression may be triggered by certain types of anxiety disorders.

Knowing this, I identified the following problem statement: Can we properly categorize posts about anxiety and depression, given that there may be significant overlap between the two.

Before modeling, I noted that there is a form of 'self-selection' when posting to a specific sub-reddit--Based on their own experience, authors are posting descriptions based on where they feel it is appropriate, even if their posts is more consistent with those in a different class.

To acquire the data, I used the PushShift API to pull data from the Depression and Anxiety subreddits. Per the API documentation, the maximum pull size is 500 posts, so I conducted 4 pulls from each subreddit to obtain 4000 posts in total, before any data cleaning.

Upon cleaning, I identified 187 posts (of 4000) included the text ‘[removed]’ or ‘[deleted]’ in place of a typical post, and I removed these prior to modeling.

As part of the exploratory data analysis, I noted that there was significant overlap in the most frequent words forr each class. I incorporated SKlearn's list of English stop words, but did not add to this list as I wanted to capture any "filler" words a post may have, given that Individuals who exhibit anxiety or depression tend to speak (and write?) using filler words—(e.g., “just”, “like”, “really”, “think”)--and I wanted these to be included in the model.

I prepared 4 primary models, including construction of pipelines and employing grid searches to identify the best parameters for a model:

Applied a Word Lemmatizer to text data and used Logistic Regression model to classify posts with Grid Search
Used Logistic Regression model WITHOUT Lemmatization to classify posts with Grid Search
Applied TFIDFVectorizer and used a Naïve Gaussian Bayes Model
Bagging Classifier with CountVectorized Features
Overall, model #2 performed the best and provided information to derive valuable insights. Model #3 performed the worst and exhibit the highest variance between the training and testing data. Model #4 exhibited the best overall performance on training data, but exhibits some variance when compared to the testing data.

The logistic regression without lemmatization was extremely valuable to identify words most important to an accurate Classification. Not surprisingly the most important words were "anxiety," "depression," "anxious," and "depressed."

Where a post was misclassified, it was easy to see why the model predicted a certain class. For example, the following post was predicted anxiety, but the true class was depression:

    'relationship with my parents, friendships, whenever I date someone, it’s all toxic. Im shy (mostly from anxiety), have low self-esteem, scared of change, scared of standing up for myself, etc etc. it sucks'

Based on the text of the post above, especially in relation to the corpus of other documents from the anxiety subreddit, it is understandable why the model predicted anxiety--but here we see one of the problems described above in our problem statement:

Not only are there overlapping categories, but post authors are self-selecting into a subreddit by stating in effect "I feel X, so I will post in X class" without considering if their post relates to the majority of the others in a subreddit.

Overall, I was positively surprised by the model performance, and believe that building an NLP tool such as this can be a first step in assisting medical professionals with taking patient statements and using these to provide diagnostic assessments of patients.

Notwithstanding the potential benefits of such an approach, there are ethical questions that must be considered for an analysis like this. Namely,

- some users appear to be treating these subreddits as an anonymous online journal. These reveal their own personal thoughts and users are likely not considering someone may read them with an ulterior motive in mind.
- Despite good intentions of using this as a medical tool, is ethical to train a model to read posts?
- The posts contain "author" tags that are ostensibly anonymous, but raise a question about whether a user's identity can be unmasked. 
- If used in a broader model, will steps be taken to anonymize the data, or what steps will a data analyst take to ensure confidentiality is maintained around personally identifiable information?
