# Wrangle WeRateDog Twitter DataSet

This project is completed for Udacity's Data Analyst Nanodegree. 

The data wrangling process consists of three main parts -- gathering, assessing and cleaning. Let's see what this project contains one by one.

## Gathering

There are three given datasets for this project.

- Archive data downloaded by the @WeRateDogs twitter account.
- Twitter API data live from Twitter
- Udacity's image predictions for the tweet images.

We have to gather these data from different sources. The archive data was provided as a CSV file by the Udacity team. This is stored locally, so no need to make any API or HTTP calls. To read this, I used the .read_csv method provided by Pandas.

The Twitter API data is provided in two ways. The first is to fetch JSON from the API using the tweepy library. The second is, in case the Twitter access is not allowed, the Udacity course team provided the downloaded JSON data in a text (txt) file. From the two, I used the latter because I couldn't get access to Twitter API. But the method on how to fetch the data is provided in the code Notebook. I had to read the file and create a DataFrame out of that (because the JSON isn't right to be represented in DataFrame format automatically).

The image predictions data is stored in Udacity's servers as a TSV (tab separated values). To read this, I used the request library to fetch the data and store it locally. Then I used the Pandas .read_csv method, but using tab (\t) as delimiter.

All the above data are stored locally.

## Analyzing

Assessments are done for

- Quality (data cleaness)
- Structure (tidyness)

I used both the visual and programmatic methods to assess the three DataFrames. For quality issues, there were two rows missing in the API data that were present in the archive data, some columns have wrong data types (time related fields were stored as string, etc.), some archive data rows were not rating (some were retweets or replies to posts; sometimes charity GoFundMe tweets), all ratings with decimal point were not correctly parsed from the tweet text, some tweets have more than one dog stages, and the image predictions were using underscore for text separation (instead of space). All the above dirtiness issues need to be cleaned.

For structural issues, the archive table was pivoted (row based data is represented as columns) and the three DataFrames hold similarly related data (the archive, API and image prediction data are representing the same entity) and hence need to be merged into one DataFrame.

## Cleaning

The following were the cleaning strategies and methodologies followed. When cleaning, I defined the problem, coded the cleaning, and tested if the cleaning was a success or not. The definition is always in plain English, but the code-cleaning and testing usually involve technical coding. For the cleaning code, I used different techniques (most of them using Pandas and NumPy libraries). The testing involves either usually programmatically asserting or visually assessing or both.

Before starting the cleaning, I copied the data so that my cleaning won't mess the original data. After cleaning, I applied different techniques to clean the copied data. For example, I deleted some rows from the archive data which were not in the API data, converted some data types from string to datetimes and numbers to strings, removed rating unrelated rows from the archive data (including retweets and replies), correctly captured decimal point ratings, etc. These were all for cleaning the dirty data.

For making the data tidy, I merged all data into one main DataFrame because they both represent the same data (tweet data). I also unpivoted (melted) the dog stages from the archive data. Unpivoting means converting column based representations to row based representation.

## Storing

The cleaned main DataFrame (the combination of the archive, API, and predictions data) need to be stored locally. Hence, I stored the csv file named twitter_archive_main.csv (I used *_main because the word master is currently discouraged in Computer Science because it is offensive!
