# Object Schema
There are several object types that are used in the community detection, embedding
generation, or other downstream tasks. Here we outline the most important 
fields present in each object and their primary usage.

## Article
Article objects are created from crawling the source websites.

### Raw
The following shows the raw data that is collected per article.

| Attribute      | Always passed | Type    | Description                       | Usage               |
|----------------|---------------|---------|-----------------------------------|---------------------|
| title          | Yes           | string  | Article title                     | Embedding input     |
| author         | Yes           | string  | Article author                    | Community detection |
| url            | Yes           | string  | Article url                       | Community detection |
| article        | Yes           | string  | Article text                      | Embedding input     |
| author_wording | Yes           | string  | Non quote sections of the article | -                   |
| nb_comment     | Yes           | integer | Number of article comments        | -                   |
| date           | Yes           | date    | Article date                      | Sorting / Indexing  |
| links          | -             | list    | urls found in the article         | -                   |
| sources        | -             | list    | Root urls of links                | -                   |

### Processed
In addition to the raw fields, each article is processed to provide the following supplemental fields.

| Attribute           | Always passed | Type    | Description                     | Usage                         |
|---------------------|---------------|---------|---------------------------------|-------------------------------|
| preprocessed_title  | Yes           | string  | Normalized article title        | Embedding input               |
| preprocessed_txt    | Yes           | string  | Normalized article text         | Embedding input               |
| conllFormat         | Yes           | string  | Article text for coNLL format   | Embedding input               |
| word_embedding_text | Yes           | string  | Article text for word2vec       | Embedding input               |
| dependencies        | Yes           | list    | Syntactic dependency per word   | Features / Analysis           |
| comment_length      | Yes           | integer | Article word count              | Features / Analysis           |
| has_hs_keywords     | Yes           | boolean | HS keyword presence             | Features / Sorting / Analysis |
| hs_keyword_matches  | Yes           | list    | List of present HS keywords     | Features / Analysis           |
| hs_keyword_count    | Yes           | integer | Count of HS keywords            | Features / Analysis           |
| unknown_words       | Yes           | list    | List of out of vocabulary words | Features / Discovery          |

## Tweet
A tweet object is for the most part the same as described in the [API](https://developer.twitter.com/en/docs/tweets/data-dictionary/overview/tweet-object).
However, for space considerations, we modify and remove several fields. 

### Raw
For simplicity, we describe only the fields we retain.

| Attribute                 | Always passed | Type    | Description                                                         | Usage                      |
|---------------------------|---------------|---------|---------------------------------------------------------------------|----------------------------|
| created_at                | Yes           | date    | Tweet date                                                          | Indexing                   |
| id_str                    | Yes           | string  | Tweet identifier                                                    | Indexing                   |
| text                      | Yes           | string  | Tweet text                                                          | Embedding Input            |
| source                    | Yes           | string  | Device / origin used to send tweet                                  | Features                   |
| in_reply_to_status_id_str | No            | string  | If tweet is a reply: ID of origin tweet                             | Community detection        |
| in_reply_to_user_id_str   | No            | string  | If tweet is a reply: ID of origin user                              | Community detection        |
| in_reply_to_screen_name   | No            | integer | Number of article comments                                          | Community detection        |
| user                      | Yes           | object  | User object                                                         | Features                   |
| coordinates               | No            | object  | Geographic origin of tweet                                          | Features                   |
| place                     | No            | object  | Geographic place attached to tweet                                  | -                          |
| quoted_status_id_str      | No            | string  | If tweet is a quote: ID of origin tweet                             | Community detection        |
| is_quote_status           | Yes           | boolean | Indicates whether this is a quoted tweet                            | -                          |
| quoted_status             | No            | object  | Tweet of origin tweet if current is a quote                         | -                          |
| retweeted_status          | No            | object  | Tweet of origin tweet if current is a reply                         | -                          |
| quote_count               | No            | integer | Indicates how times tweet has been quoted                           | Features                   |
| reply_count               | Yes           | integer | Number of times this Tweet has been replied to                      | -                          |
| retweet_count             | Yes           | integer | Number of times this Tweet has been retweeted                       | -                          |
| favorite_count            | No            | integer | Indicates how many times this Tweet has been liked by Twitter users | -                          |
| entities                  | Yes           | object  | Stores hashtags, mentions, urls, etc                                | Features / Embedding input |
| extended_entities         | No            | object  | Stores attached media                                               | -                          |
| lang                      | No            | string  | ML detected language                                                | Indexing                   |

### Processed
Tweets are processed to provide the following supplemental fields.

| Attribute           | Always passed | Type    | Description                     | Usage                         |
|---------------------|---------------|---------|---------------------------------|-------------------------------|
| hashtags            | No            | list    | Extracted hashtags              | Features / Embedding input    |
| user_mentions       | No            | list    | Extracted user_mentions         | Features                      |
| urls                | No            | list    | Extracted urls                  | Features                      |
| media               | No            | list    | Extracted media                 | -                             |
| preprocessed_txt    | Yes           | string  | Normalized article text         | Embedding input               |
| conllFormat         | Yes           | string  | Article text for coNLL format   | Embedding input               |
| word_embedding_text | Yes           | string  | Article text for word2vec       | Embedding input               |
| dependencies        | Yes           | list    | Syntactic dependency per word   | Features / Analysis           |
| comment_length      | Yes           | integer | Article word count              | Features / Analysis           |
| has_hs_keywords     | Yes           | boolean | HS keyword presence             | Features / Sorting / Analysis |
| hs_keyword_matches  | Yes           | list    | List of present HS keywords     | Features / Analysis           |
| hs_keyword_count    | Yes           | integer | Count of HS keywords            | Features / Analysis           |
| unknown_words       | Yes           | list    | List of out of vocabulary words | Features / Discovery          |