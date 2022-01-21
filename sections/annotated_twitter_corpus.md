


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


## Python

We will be using the twarc library in Python

```Bash
pip3 install twarc
```
### Prerequisites
To crawl tweets you will need to have a set of keys and tokens to authenticate your request. You can generate these keys and tokens by following these steps:

1. Sign up for a developer account and receive approval.
2. Create a Project and an associated developer App in the developer portal.
3. Navigate to your App's “Keys and tokens” page to generate the required credentials. Make sure to save all credentials in a secure location.


### Lookup Tweets using Tweet IDs

```python
# This will import the Twarc2 client and expansions class from twarc library and also the json library
from twarc import Twarc2, expansions
import json

# This is where you initialize the client with your own bearer token (replace the XXXXX with your own bearer token)
client = Twarc2(bearer_token="XXXXX")


#Once you have initialized the client, and imported the expansions class and the json library, you are ready to get Twitter data using the Twitter API v2.



def main():
    # List of Tweet IDs you want to lookup
    tweet_ids = ['1404192093803741184', '1403738886275096605', '1397216898593525762']
    # The tweet_lookup function allows 
    lookup = client.tweet_lookup(tweet_ids=tweet_ids)
    for page in lookup:
        # The Twitter API v2 returns the Tweet information and the user, media etc.  separately
        # so we use expansions.flatten to get all the information in a single JSON
        result = expansions.flatten(page)
        for tweet in result:
            # Here we are printing the full Tweet object JSON to the console
            print(json.dumps(tweet))


if __name__ == "__main__":
    main()


```


## I cannot download the tweets, what can I do?

Please send an email to shamsuddeen2004@gmail.com and I will gladly assist you in obtaining the dataset.

