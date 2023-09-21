# Spotify-Data-Stream-Pipeline-to-Snowflake-via-AWS
In this project, we will fetch data from spotify API using the Spotipy module and store the transformed data to Snowflake

#Step 1:
We will create our app on developers.spotify.com, this will give us secret id and secret key to fetch data from spotify. We need to create one AWS Lambda function which will fetch the data from spotify API. We need to upload Spotipy zip file to our Lambda function layer as it is not available in native AWS environment. On top of this Lambda function, we will create one AWS cloudwatch trigger which will run every 1 hour. This will execute the lambda function every one hour. That data will be stored in S3 bucket created to store the raw data.

#Step 2:
Once our extract Lambda function fetches the data from API to S3 bucket, it is in raw format. We need to transform the raw JSON we received. We will create 3 dataframes from the raw json - Artist DF, Album DF and songs DF. For this we will write one lambda function, which will parse the json data and create these 3 dataframes. We will store the data in CSV format. To execute this lambda function, we will create another trigger on raw data S3 bucket, whenever data arrives in the raw S3 bucket, this transformation lambda function will be triggered. This will store the created dataframes in the a separate folder inside the same bucket.

# Step 3:
Once the data is arrived in curated S3 bucket, it needs to be loaded onto Snowflake. For this we will build a snowpipe on this bucket which will load the data to snowflake. Once the data is in snowflake, you can use snowflake's compute resources to query that data, build visualizations out of it.

**You can find all these scripts in repository.
