# Zé Lensky Dataset (ZLDB) - Processed JSONL Release

## 1. Overview

The **Zé Lensky Dataset (ZLDB)** is a large-scale collection of Brazilian Portuguese Twitter data related to the Russia-Ukraine conflict. It spans from **January 1, 2022** onwards, capturing public discourse, stance, sentiment, and related social media dynamics.

This release provides the **processed metadata** of the dataset in `.jsonl` format. All tweet text content has been removed to comply with Twitter’s Developer Policy. Researchers can **rehydrate** the original text and user profile information using the included tweet IDs.

After STIL, we will add the rest of the content here (including the citation format for the paper, and others.)


## 2. File Structure

The dataset is composed of jsonl files stored as:

```
ZL/processed_jsonl/
├── zldb_records_2022_01_01.jsonl
├── zldb_records_2022_01_02.jsonl
└── ...
```

Each row of the jsonl refers to a single tweet (record)


## 3. Record Schema

Each record has the following structure (mock example):

```json
{
  "zldb_raw_id": "zldb_record_4902796509317840896",
  "timestamp": "2022-01-01T23:59:42.000Z",
  "verified": true,
  "comments": 12,
  "retweets": 4,
  "analytics": "engagement: high",
  "tags": ["politics", "ukraine"],
  "mentions": ["@user1", "@user2"],
  "emojis": ["🇧🇷", "🔥"],
  "tweet_id": "1874243945527730366",
  "zldb_user_id": "zldb_user_a94f0c3d",
  "analysis": {},
  "filter": {},
  "content_tokens": {}
}
```

Each field corresponds to the following:

* **zldb_record_id**: Internal dataset identifier, but based on thw tweet id (`zldb_record_[tweet_id]`).
* **timestamp**: Original tweet timestamp (ISO 8601).
* **verified**: Boolean flag for verified accounts.
* **comments**: Number of replies.
* **retweets**: Number of retweets.
* **analytics**: Engagement metadata (string, format varies).
* **tags**: Extracted hashtags.
* **mentions**: Extracted user mentions.
* **emojis**: Extracted emojis.
* **tweet_id**: Original Twitter ID.
* **zldb_user_id**: Anonymized user identifier (`zldb_user_[hash]`).
* **analysis**: Object reserved for stance/sentiment or other future annotations.
* **filter**: Object reserved for preprocessing flags.
* **content_tokens**: Object reserved for tokenized representations (e.g., BERT, RoBERTa).

## 4. Rehydration

To comply with Twitter’s Developer Policy, tweet content has been removed. Researchers who wish to access the original text must **rehydrate** the dataset using the `tweet_id` field. The steps for rehydratation are:

1. Obtain approved access to the Twitter/X API.
2. Use the `tweet_id` values to query the API and fetch the full tweet objects.

   * Example (using Tweepy in Python):

     ```python
     import tweepy

     client = tweepy.Client(bearer_token="YOUR_BEARER_TOKEN")

     tweet_ids = ["1874243945527730366", "1874243945527730367"]
     tweets = client.get_tweets(ids=tweet_ids, tweet_fields=["created_at","author_id","public_metrics"])
     ```
3. The returned tweet objects can be merged with the processed metadata to restore a more complete dataset.

## 5. Ethical and Legal Considerations

* **Content policy**: This release does not distribute raw tweet text, in line with Twitter/X’s terms. Only tweet IDs and derived metadata are provided.
* **User privacy**: User handles have been anonymized.
* **Rehydration**: Access to tweet text requires a valid Twitter/X API key and is subject to Twitter’s terms of service.
* **Archival stability**: Some tweets may no longer be available due to deletion, suspension, or other reasons.

## 6. Intended Use & Contact

This dataset is intended for **academic and research purposes**, especially in areas such as:

* Stance detection
* Sentiment analysis
* Discourse analysis
* Political communication
* Social media studies

In case of doubts, suggestions, or problems reproducing or expanding the data, you can contact the corresponding author at: `andreispurim@proton.me`
