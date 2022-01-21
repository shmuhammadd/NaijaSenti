


## Manually Annotated Twitter Sentiment corpus

We manually annotated the Twitter sentiment corpus in four major Nigerian languages (Hausa, Igbo, Nigerian-Pidgin, and Yoruba). We realese the dataset with the following metadata for each language: the number of positive, negative, and neutral classes. We also manually annotated the dataset and classified the tweets if they were code-mixed (e.g., a mix of Hausa and English or Hausa and Yoruba) or monolingual.

| Languages |      #positive |      #negative| #neutral |  #code-mixedd  | #mono-lingual | 
| --------- | -------- |  -------- | -------- |  ---------- | ---------- |
| Hausa  |    9,235    |  9,033  | 12,826  |  6,426  | 21,039   | 
| Igbo  |  5,621  |  4,726 | 14,887  |  6,561  |  8,688  |
| Pidgin  | 3,010  |  5,635  |  717 |  -  | -  |
| Yoruba  | 9,839  |  5,003  | 14,356  |  4,457  | 18,622  | 




## How to download the dataset?

Twitter has a strong policy for public distribuition of user data. Below is an excerpt from [Twitter policy](https://developer.twitter.com/en/developer-terms/agreement-and-policy). 


> The best place to get Twitter Content is directly from Twitter. Consequently, we restrict the redistribution of Twitter Content to third parties.  If you provide Twitter Content to third parties, including downloadable datasets or via an API, you may only distribute Tweet IDs, Direct Message IDs, and/or User IDs (except as described below). We also grant special permissions to academic researchers sharing Tweet IDs and User IDs for non-commercial research purposes.


So, we cannot not share the entire Tweet text directly. Instead, we can only share a list of Tweet IDs. Researchers can then use the Twitter API to hydrate and get the full Tweet objects from the Tweet IDs. We provide python and R code to allow hydrating all the tweets in our dataset. If you have any trouble, please send an email to shamsuddeen2004@gmail.com and I will gladly assist you in obtaining the dataset.



## Hydrating Tweets using Tweets IDs. 

Our corpus was built using Twitter API v2 which allow access to historical Tweets from the entire archive of public conversation on Twitter, dating back to 2006 (using the full-archive search endpoint). However, Twitter API v2 is for academic researchers and you can apply here:[academic research product track](https://developer.twitter.com/en/products/twitter-api/academic-research)


## Prerequisites

To crawl tweets you will need to have a set of keys and tokens to authenticate your request. You can generate these keys and tokens.
See the following for more information on how to generate these keys
1. [Getting your keys and bearer token from the developer dashboard](Getting your keys and bearer token from the developer dashboard)
2. [How to get access to the Twitter API
](https://developer.twitter.com/en/docs/twitter-api/getting-started/getting-access-to-the-twitter-api)




## Hydrate Tweets using Tweet IDs in Python

We will be using the [twarc](https://github.com/DocNow/twarc) library in Python. More info on using [twarc](https://twarc-project.readthedocs.io/en/latest/twarc2_en_us/)


```bash

#Open up a new terminal and install twarc v2 
pip3 install --upgrade twarc

```
>Once you've got your Twitter developer access set up you can tell twarc what they are with the configure command

```bash
twarc2 configure
```
> twarc's hydrate command will read a file of tweet identifiers and write out the tweet JSON for them using Twitter's tweets API endpoint:

```bash
twarc2 hydrate ids.txt tweets.jsonl

```
> The input file, ids.txt is expected to be a file that contains a tweet identifier on each line, without quotes or a header suh as:

```
919505987303886849
919505982882844672
919505982602039297
```

### Processing data into common analysis formats

The resulting file is a data type called JSON, which has many advantages for moving large amounts of structured data. However, we need to take some steps to transform the JSON into a form more common for data analysis. We can use the twarc-csv module to convert the line oriented JSON to CSV which then should be more easy to use as DataFrames in tools like Pandas and R. Twarc plugins are distributed separately from twarc, and they extend the base twarc2 command with additional subcommands, in the case of twarc-csv a csv subcommand will be added.

```python

# install  twarc-csv
pip3 install --upgrade twarc-csv

 # convert to CSV
twarc2 csv tweets.jsonl tweets.csv

import pandas

pandas.read_csv('tweets.csv')# load the CSV into a Pandas DataFrame:

```
## Hydrate Tweets using Tweet IDs in R


For R users, you can use the [academicTwitteR](https://github.com/cjbarrie/academictwitteR) package in R. All the code can be found here. Install the academicTwitteR first:


```R

# Install academicTwitteR package
install.packages("academicTwitteR")


# This will load the academicTwitteR package
library(academictwitteR)

# Set your own bearer token (replace the XXXXX with your own bearer token)
bearer_token <- "XXXXX"


hydrate_tweets(
  ids = c("919505987303886849", "919505982882844672", "919505982602039297")
  bearer_token = bearer_token,
  data_path = "path",
  bind_tweets = TRUE,
  verbose = TRUE
)

```



## I cannot download the tweets, what can I do?

Please send an email to shamsuddeen2004@gmail.com and I will gladly assist you in obtaining the dataset.

