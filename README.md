# How to Set Up an NBA Data Lake with AWS services
simple py script to automate the creation and querrying of a data lake for NBA analytics using AWS services..hands on tho
The datalake_nba.py script actually does thethe following tasks:

- Creates an Amazon S3 Bucket: This bucket is used to store both raw and processed data.
- Uploads Sample NBA Data: JSON-formatted data is uploaded to the S3 bucket.
- Sets Up AWS Glue: A Glue database and an external table are created for querying the data.
- Configures Amazon Athena: Enables querying of data stored in the S3 bucket.

# Requirements needed
Before running the script, ensure you have the following:

Sportsdata.io API Key:

- Sign up for a free account at Sportsdata.io.
- Navigate to Developers > API Resources > Introduction & Testing.
- Select the "SportsDataIO API Free Trial" and complete the form, choosing NBA for this tutorial.
- Check your email for a link to the "Developer Portal."

Now look into the portal, switch to NBA, scroll to "Standings," and locate the API Key under "Query String Parameters."
Copy this key for later use.

IAM Role/Permissions:

- Ensure the user or role executing the script has the following permissions:
S3: s3:CreateBucket, s3:PutObject, s3:DeleteBucket, s3:ListBucket
- aws Glue: glue:CreateDatabase, glue:CreateTable, glue:DeleteDatabase, glue:DeleteTable
- Athena: athena:StartQueryExecution, athena:GetQueryResults
 


 # Steps to Set Up the environment
- Step 1: Open CloudShell
- Log in to your AWS account at aws.amazon.com.

Now in the top navigation bar, click the square icon with >_ to open CloudShell.

- Step 2: Create the setup_nba_data_lake.py Script#

In the CLI, run the following code:

```
nano setup_nba_data_lake.py

```

In a separate browser tab, open the GitHub repository containing the script.
Copy the script contents and paste them into the CloudShell editor.
Locate the line under # Sportsdata.io configurations that mentions api_key. Paste your API key into the quotation marks.

Save and exit:
Press Ctrl + X to exit, then Y to save changes, and presss Enter key to confirm the file name.


Step 3: Create the .env File

```bash
nano .env
```

2. paste the following line of code into your file, ensure you swap out with your API key

```bash
SPORTS_DATA_API_KEY=your_sportsdata_api_key
NBA_ENDPOINT=https://api.sportsdata.io/v3/nba/scores/json/Players
```

Save and exit as described in Step 2.

# Step 4: Run the script
1. In the CLI type
```bash
python3 datalake.nba.py
```
-Expect see the resources were successfully created, the sample data was uploaded successfully and the Data Lake Setup Completed


# Step 5: Manually Check For The Resources

S3 Bucket:
- Open the S3 console and locate the newly created bucket, typically named Sports-analytics-data-lake.
- Navigate into the bucket:
- check the raw-data folder for the file nba_player_data.json.
- Open the file to confirm it contains NBA data.

4. Head over to Amazon Athena and you could paste the following sample query:
```bash
SELECT FirstName, LastName, Position, Team
FROM nba_players
WHERE Position = 'PG';
```


# What This Tutorial Coverered

- Setting up AWS services with least-privilege IAM policies.
- utomating resource creation with Python scripts.
- Integrating external APIs into cloud workflows.

# Future Improvements
Automate data ingestion using AWS Lambda.
Add data transformation capabilities with AWS Glue ETL.
Enhance analytics and visualizations using AWS QuickSight.






