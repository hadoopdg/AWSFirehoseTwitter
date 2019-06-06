# Listed details below gives the information about the configuration file and the python code
1. accessConfig.py : This configuration file contains the access credentials details to connect to Twitter account 
consumer_key = '<consumer key of the app registered under your account>'
consumer_secret = '<consumer secret key of the app registered under your account>'
access_token =  '<access token of the app registered under your account>'
access_secret = '<access secret token of the app registered under your account>'

We are going to import this file into getBatchData.py which is our main script that pull data and pushes out to Kinesis Firehose.

2. getBatchData.py :  
First we are going to import all the necessary packages along with the accessConfig. 
The api variable is now our entry point for most of the operations we can perform with Twitter. 
For this project purpose we are going to filter and pull all the tweets with a particular hashtag that is of our interest. 
I have chosen ‘DonaldTrump‘ so that I can perform Sentiment analysis on the data pulled 

In the  code we are doing a ‘search‘ query with filter queryHashtag applied to search results and we are requesting 100 items
to be returned in the response.

Now, the response for the search query contains 100 tweets.We are taking each tweet from 100 tweets and then passing that tweet
to a function called process_or_store which pushes to the Kinesis firehose.For that we need to initialize our firehose client.
Firehose_client is the variable that we use to access Kinesis Firehose.

Additionally I have also initialized logging and all the logs are stored in tmp directory with the filename DataAnalysisOnAWS.
log We are going to store all DEBUG messages in the log file. 

Once, the firehose client is created, we are going to use it in the process_or_store function. 
From the tweets we retrieved earlier, we are passing each tweet as a variable to this function. 
In this function, we simple push the tweet to a Kinesis Firehose delivery stream. 
Using while True ( indicates that it is a never ending loop) calling def main() which pull 100 tweets and pushes to Kinesis Firehose.
