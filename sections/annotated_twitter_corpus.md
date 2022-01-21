


## Manually Annotated Twitter Sentiment corpus

We manually annotated the Twitter sentiment corpus in four major Nigerian languages (Hausa, Igbo, Nigerian-Pidgin, and Yoruba). We realese the dataset with the following metadata for each language: the number of positive, negative, and neutral classes. We also manually annotated the dataset and classified the tweets if they were code-mixed (e.g., a mix of Hausa and English or Hausa and Yoruba) or monolingual.

| Languages |      #positive |      #negative| #neutral |  #code-mixedd  | #mono-lingual | 
| --------- | -------- |  -------- | -------- |  ---------- | ---------- |
| Hausa  |    9,235    |  9,033  | 12,826  |  6,426  | 21,039   | 
| Igbo  |  5,621  |  4,726 | 14,887  |  6,561  |  8,688  |
| Pidgin  | 3,010  |  5,635  |  717 |  -  | -  |
| Yoruba  | 9,839  |  5,003  | 14,356  |  4,457  | 18,622  | 


## How to download the dataset?

Twitter has a strong policy for public distribuition of user data. According to [Twitter policy](https://developer.twitter.com/en/developer-terms/agreement-and-policy), we cannot not share the entire Tweet text directly. Instead, we can only share a list of Tweet IDs. Researchers can then use the Twitter API to hydrate and get the full Tweet objects from the Tweet IDs.

```
The best place to get Twitter Content is directly from Twitter. Consequently, we restrict the redistribution of Twitter Content to third parties.  If you provide Twitter Content to third parties, including downloadable datasets or via an API, you may only distribute Tweet IDs, Direct Message IDs, and/or User IDs (except as described below). We also grant special permissions to academic researchers sharing Tweet IDs and User IDs for non-commercial research purposes.
```

So, we only share the Tweet IDs of the annotated tweets and  python and R code to allow hydrating all the tweets in our dataset. 

### Step
You only need three things:

1. The script 'NaijaSenti.py';
2. The python-twitter library - well, maybe you will need more libraries... I am not sure;
3. A valid Twitter API key. You need this because technically you are downloading the data on your own, I only labeled the tweets I don't own them.


1. Make sure you have your bearer token from an app connected to your academic research project, as shown in module 4

2. pip3 install twarc

```python

# This will import the Twarc2 client and expansions class from twarc library and also the json library
from twarc import Twarc2, expansions
import json

# This is where you initialize the client with your own bearer token (replace the XXXXX with your own bearer token)
client = Twarc2(bearer_token="XXXXX")


from twarc import Twarc2, expansions
import json

# Replace your bearer token below
client = Twarc2(bearer_token="XXXXX")


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


## I cannot download the dataset, what can I do?

I can not download the tweets, or the running codes do not work, where do I go? You can send an e-mail for shamsuddeen2003@gmail.com and I will be happy to answer any questions and help anyway I can. :D



