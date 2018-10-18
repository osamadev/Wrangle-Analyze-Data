# Warngle and Analyze Data
In this project, we will wrangle and analyze data collected from a twitter account for rating dogs called "WeRateDogs". The data includes a text of the tweets on that twitter account in addition to other attributes such as "Id" of the tweet, the time stamp, retweet status...etc. Also there are some other fields have been extracted from the tweets text such as the rating of each dog, its name, and the stage (doggo, floofer, pupper, or puppo).

# Gathering Data
This step is our first step in the data wrangling process. In this step, we gather the required data from different sources, mainly we have three sources as follows:

-  The excel file provided by Udacity and I have downloaded right away from the link on the project description page.
-  The tweets that will be queried directly from Twitter API to get more information and additional fields about the tweets using the twitter_id field from the given Excel sheet.
-  The "image-predictions.tsv" file that includes the images' predictions and we have to get and download its content from the given URL through a direct web request call.


## Finding out Quality and Tidiness issues
**Let's start with the quality issues. After exploring the data, I have found the following quality issues:**

In "tweets_archive_df" dataframe:, we have the following quality issues:

-  There are rows in "tweets_archive_df" dataframe that represent retweets, not original tweets, so these rows should be deleted because they're not original tweets. As indicated above from "retweeted_status_id" field, there are 181 rows in "tweets_archive_df" dataframe are retweets and they will be removed.

-  Some of dog names in "name" field are missing or mislabeled. The reasons for this issue is either due to the dog name was not mentioned in the tweet text itself, or due to a problem in the pattern or the way used to extract the dog name from the text. That is why we found "None" in the "name" field in some cases and also wrong names such as "a, all, an, such, just, O, quite, not, one...etc." in some other cases.

-  If the dog name in the "text" field consists of multiple words, it will be labeled incorrectly (mislabeled) in the "name" field.

-  There are some unwanted columns in this dataframe that need to be dropped or removed as they're not important for our analysis task.
There are 23 records where the "rating_denominator" field has values other than 10, such as "0, 2, 7, 11, 12, 150, 170...etc.". These numbers are wrong because the rating denominator should be always "10". The root cause of this issue is either wrong extraction from the tweet text, or wrong rating given by the user who wrote this tweet.
In "tweets_df" dataframe:, we have the following quality issues:

-  "id" field needs to be renamed to "tweet_id" to match the other two dataframes.
-  There are many unwanted columns should be excluded (dropped), as they're not important for our analysis task.
-  There are rows in "tweets_df" dataframe which are also retweets and need to be removed from the dataframe as they're not original ones. As inicated above from "retweeted_status" field, there are 167 rows or observations in "tweets_df" dataframe are retweets and they will be also removed.
-  In "img_predictions_df" dataframe:, we have the following quality issues:

-  Remove "" underscore from the dog breed fields "p1, p2, p3" to make the breed name more readable and consistent.
-  Some of values in "p1, p2, p3" columns start with capital letters and others with small letters, we need to make these values more consistent.

**Now let's explore some of the tidiness issues in the data.**

In "tweets_archive_df" dataframe:, we have the following issues:

-  "timestamp" field need to be splitted into two fields, date field and time field.
-  The "doggo, floofer, pupper, puppo" fields will be combined into one field, let's call it "stage" field. The reason for that is to have a real variable rather than values in the header.
-  Drop unwanted columns, then re-order the desired remaining columns in more logical sense.
-  The rating fields "rating_numerator & rating_denominator" need to be float, not integers.
In "tweets_df" dataframe:, we have the following quality issues:

-  Drop unwanted columns, then re-order the desired remaining columns in more logical sense to be more readable.

## analyzing, and visualizing the wrangled data
**we can conclude the following insights about the dataset:**

-  The total number of observations in the dataset is 1993 rows.
-  The mean or average of the favorites count (likes) is 8794.24, the median is 3988, and the maximum is 165056
-  The mean or average of the rating is 12.28/10.53, the median rating is 11/10, and the maximum is 1776 (this maximum is appearantely an outlier in the data).
-  The mean or average of the reweets count is 2681.1, the median value is 1290, and the maximum is 84452
-  The average number of images with each tweet is one image, median value is also one image, and the maximum is 4
-  The mean or average value of the confidence level of the first most likely prediction is about 0.59 (59%) and the median is very close to the average 0.587 (58.7%)

