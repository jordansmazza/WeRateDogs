# WeRateDogs
##### By Jordan Mazza

## Introduction
In this project, I use three datasets (one local dataset, one downloaded programaticially, and one taken from Twitter's API), each describing different aspects of the Twitter account WeRateDogs. This account is known for posting photos of dogs of all ages and breeds and rating them out a unique rating system.

## Assessing Cleanliness of Data
##### Quality
- **Tweets Archive**
  - includes replies, and retweets as seen by `in_reply_to_user_id` and `retweeted_status_user_id` columns (only want original tweets)
  - invalid data in `rating_denominator` column (anything other than 10)
  - `tweet id` column datatype datatype could be str instead of int (it is a name)
  - `timestamp` column datatype should be datetime not str
  - some missing values in `name` column marked under 'a' and others 'None'
- **Twitter Image**
  - `p1`, `p2`, and `p3` columns have underscores instead of spaces
  - `tweet id` column datatype datatype could be str instead of int
  - there are 2075 rows in this dataframe and 2356 rows in the archive dataframe
- **Tweets Dataframe**
  - `tweet_id` column datatype could be str instead of int
  - some retweet counts and favorite counts seem low (most likely these are retweets and replies)
  - there are 2331 rows in this dataframe and 2356 rows in the archive dataframe
##### Tidiness
- **Tweets Archive**
  - columns relating to retweet and reply data is irrelevant (we only want original tweets)
  - `dog_stage` data is broken up into 4 columns when should be in 1
- **Twitter Image**
  - this dataframe is tidy
- **Tweets Dataframe**
  - this dataframe is tidy

The first thing I noticed while assessing the data was the retweet and replies data. Sincde we only want original tweets in this analysis, I only saved the rows that had null values in the columns for retweet and reply status id. I noticed some strange inputs for the denominators and numerators, but after filtering through this data, I found it unnecessary to remove the strange variables in the numerator column for two reasons. First, some tweets included many dogs and so the numerator rating was incredibly high. Second, account’s rating system developed over time to what it is today, so some of the early tweets included a standard rating system out of ten. 

For the denominator, there were only 17 rows with strange data, so I went through them manually and found some of the ratings incorrectly interpreted the text. For example, one tweet listed the date 7/11 in the text, and the denominator rating was 11. I removed these using the .drop() function to drop their specific indices. I also changed some columns to objects types that matched the data better. I also changed all the missing values in teh name column to None using .replace() to keep consistency.

I then removed all the columns relating to retweets and replies. I removed the text in all the rows with ‘None’ values in all four columns using the .replace() function. Then, I created a new column by combining all the dog stage columns. I used the str.replace() function again to fix the formatting on the rows with multiple dog stages. After checking to ensure this method worked by querying the old dog stage columns to make sure they matched the new column, I dropped the old columns.

For the twitter image dataframe, I used the .str.replace() function to replace the underscores with spaces in the p1, p2, and p3 columns. Now that all the dataframe have been assessed and cleaned, I combined them all to create one master dataframe for my analyses and stored this new dataframe to a CSV file.

## Analysis
