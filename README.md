# Create an ETL Job using AWS Glue Studio, S3, & Athena

<figure>
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTQE_gM7J-F-zJr5ENSCemdOdgMDV9iNKk7Ww&s" alt="Data warehouse representation" width=60% height=60%>
</figure>
## Background

In this project, we will walk through how to create an ETL job using the following AWS Cloud Services:
- **Amazon S3** (for intermediary data storage)
- **AWS Glue Studio** (main engine of the ETL job)
- **Amazon Athena** (query tool)

ETL stands for Extract, Transform, and Load. In almost all Enterprise IT settings, it is very common to have huge volumes of Analytical data. For that data to be consumable and used by business areas to generate insights and forecast business goals, the data needs to be:
1. **Extracted** from where it is stored/originated,
2. **Transformed** to fit a certain format (usually involves cleaning the data, removing duplicates, etc.), and then,
3. **Loaded** into the target destination source.

Very often, there is also the presence of a large data warehouse, and multiple databases/storage layers feeding data into the larger warehouse for general business consumption.

Without further ado, we will now create an ETL Job using AWS Glue (an event-driven, serverless computing service).

## Step 1 — Create an S3 Bucket
This S3 Bucket will store our data. We’re basically just building a database within the S3 Object storage service.

1. Create an S3 Bucket (keep default options when creating it).

## Step 2 — Create some Mock Data
For this step, create a quick `.csv` file with data about coffee orders. This data file will be uploaded to the S3 bucket from the previous step.

- **coffee.csv**

## Step 3 — Upload the coffee data file to the S3 Bucket
1. Upload the `coffee.csv` file to the S3 bucket.

## Step 4 — Create an IAM Role for Glue with the Required Permissions
1. Create an IAM Role with the necessary permissions for AWS Glue.

## Step 5 — Define the Glue Data Crawler in AWS Glue
AWS Glue was launched in 2017. It is a fully-managed, serverless, and AWS Cloud-optimized ETL Service offering. Using Glue, there are numerous ways to connect to our data store in S3. For this tutorial, we will use Glue Crawler. This Crawler will “crawl” the data file in our S3 bucket and create a table schema in Glue.

1. Give the crawler the name `etl-tutorial-crawler` and click **Next**.
2. Keep the default settings as is for the Crawler. Click **Next**.
3. Select **S3** for the data store, and add the name of your S3 bucket. Click **Next**.
4. Select the **Choose an existing IAM Role** radio button, and select the IAM Role created in Step 4. Click **Next**.
5. Set the frequency to **Run on Demand**. Click **Next**.
   - (Note: if required, you can always set customized scheduling for your Crawler to run on an hourly, daily, weekly, or monthly cadence).
6. Create a database `coffee-database` for storing the output from the Crawler. Click **Next**.
7. Review all settings and click **Finish** to create the Crawler.
8. Run the Crawler. If the job status updates from starting to stopping, and then to ready, the Crawler job was successful.

## Step 6 — Defining our Glue Job
Now that we have set up the Glue Crawler to point and recognize the data file in S3, we will define our Glue job to perform the ETL portion of this tutorial.

1. From the AWS Console, go to AWS Glue Studio.
2. Select **Amazon S3** as both the Source and Target. Click **Create**.
3. Set up your Glue Job.
4. Run the job. While it’s running, you should see an output.
5. After the Glue job is finished running, your output should look like this.

## Step 7 — Querying our data using Athena
AWS Athena is a query service offered by AWS that analyzes data in S3 using SQL. For this tutorial, we will run Athena to query the ETL data and run some SQL operations.

1. Go to the AWS console, and search for Athena.
2. Run the query as shown below.
3. After running the query, we should see our results.

## Overall Summary
When it comes to data engineering, ETL operations and pipelines are a huge part of it. Apart from Glue, there are a multitude of other ETL services (i.e. Cloud Air Fusion by Google Cloud, Data Factory offered by Azure, and many others). The basic idea is that it should assist with the reduction of engineering efforts required by supplying a base (source and target locations and configurations). 

We have just completed ETL using AWS Glue. My hope is that this walkthrough helps you with your projects! 

In case I missed anything, or if you have any questions/thoughts, please submit them in the comments section below.
