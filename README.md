# Sentiment-analysis---Reddit-data-on-US-elections
This Repo consists of a project on Sentiment analysis of Reddit data on US elections in 2024


<h3 align="center">Step-1:</h3>
Install Praw and word cloud in your console

!pip install praw
!pip install wordcloud

<h3 align="center">Step-2:</h3>

import the libraries in the console, In my project I have used jupyter notebook 

    code:
    import praw
    import pandas as pd
    import numpy as np
    import re #RegEx : Regular expression
    user_agent = 'to fetch and analysis'

And to fetch the data from Reddit we need the client ID 

    reddit = praw.Reddit(
     client_id = '6fx2pfa7_lNbIr7qlI9y6A',
      client_secret = '230-pSd-ILe2bDbIcIeSVFKLw3DK2A',
     user_agent=user_agent
    )

<h3 align="center">Step-3:</h3>

the function to collect the headlines from Reddit 

    def headlines(p_name):
        # Define the subreddit you want to search in
        subreddit = reddit.subreddit('politics')
    
        # Define the hashtag you want to search for
        hashtag = f'#{p_name}'
        headlines = set()
        # Search for submissions containing the hashtag
        for submission in subreddit.search(hashtag, time_filter='all', limit=500):
            headlines.add(submission.title)
        return headlines

The function is to collect the words to search in a headline

    def preprocess_text(p_name):
        headlines_set = headlines(p_name)
    
        # Convert the set of headlines into a list
        headlines_list = list(headlines_set)
    
        # Preprocess each headline
        preprocessed_headlines = []
        for headline in headlines_list:
            # Remove URLs, HTML tags, emojis, and emoticons using regex
            text = re.sub(r'http\S+|www\S+|<[^>]*>|[\U00010000-\U0010ffff]', '', headline)
    
            # Remove punctuation and special characters using regex
            text = re.sub(r'[^a-zA-Z0-9\s]', '', text)
    
            # Remove short words (length < 3) and long words (length > 15) using regex
            text = re.sub(r'\b\w{1,2}\b|\b\w{16,}\b', '', text)
    
            # Remove extra whitespace
            text = re.sub(r'\s+', ' ', text).strip()
    
            preprocessed_headlines.append(text)
    
        return preprocessed_headlines


<h3 align="center">Step-4:</h3>

Do the Data Analysis with the data found 

I have uploaded the code please refer to that for Data Analysis 


<h3 align="center">Step-5:</h3>

Conclusion :
According to the results, there will be good competition between Mr.Donald Trump and Mr.Joe Biden.
But according to the Reddit comments, Joe Biden will win the elections in 2024 in the US. 
