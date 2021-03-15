# Tweets Collection and Analysis Pipeline

This project implements a data pipeline using Docker. Tweets are streamed about sustainability are streamed via Tweepy Listener and stored in a MongoDB database. The ETL job performs live sentiment analysis (using [VADER](https://github.com/cjhutto/vaderSentiment)) on the stored tweets and loads them with the according score into a PostGres SQL database. In the end tweets with most positive sentiment are posted on Slack using a Webhook.

![Pipeline](Images/pipeline.pdf)

## Docker Compose necessities

Setting up local environmental variables
- Twitter API Access (via https://developer.twitter.com/):
  * TWITTER_API_KEY
  * TWITTER_API_SECRET
  * TWITTER_ACCESS_TOKEN
  * TWITTER_ACCESS_TOKEN_SECRET

- PostGres SQL Credentials for your database:
  * POSTGRES_USER
  * POSTGRES_PASSWORD
  * POSTGRES_DB

- SLACK API Access (via https://api.slack.com/apps):
  * SLACK_WEBHOOK (e.g https://hooks.slack.com/services/...)

## Changing streaming filter

The file `get_tweets.py` contains the Tweepy Tweets Listener. The topic filter is found at the end of the file:
 `stream.filter(track=['sustainable'], languages=['en'])`
