Load data from Cloud Storage into BigQuery
In the Console, on the Navigation menu (Navigation menu) click BigQuery then click Done.

Create a new dataset within your project by selecting your project in the Resources section, then clicking on CREATE DATASET on the right.

In the Create Dataset dialog, for Dataset ID, type logdata.

For Data location, select the continent closest to the region your project was created in. click Create dataset.

Create a new table in the logdata to store the data from the CSV file.

Click on Create Table. On the Create Table page, in the Source section:

For Create table from, choose select Google Cloud Storage, and in the field, type gs://cloud-training/gcpfci/access_log.csv.
Verify File format is set to CSV.
Note: When you have created a table previously, the Create from Previous Job option allows you to quickly use your settings to create similar tables.

In the Destination section:

For Dataset name, leave logdata selected.

For Table name, type accesslog.

For Table type, Native table should be selected.

Under Schema section, for Auto detect check the Schema and input Parameters.

Accept the remaining default values and click Create Table.

BigQuery creates a load job to create the table and upload data into the table (this may take a few seconds).

(Optional) To track job progress, click Job History.

When the load job is complete, click logdata > accesslog.

On the table details page, click Details to view the table properties, and then click Preview to view the table data.

Each row in this table logs a hit on a web server. The first field, string_field_0, is the IP address of the client. The fourth through ninth fields log the day, month, year, hour, minute, and second at which the hit occurred. In this activity, you will learn about the daily pattern of load on this web server.

Click Check my progress to verify the objective.
Load data from Cloud Storage into BigQuery

Task 3: Perform a query on the data using the BigQuery web UI
In this section of the lab, you use the BigQuery web UI to query the accesslog table you created previously.

In the Query editor window, type (or copy-and-paste) the following query:

Because you told BigQuery to automatically discover the schema when you load the data, the hour of the day during which each web hit arrived is in a field called int_field_6.

select int64_field_6 as hour, count(*) as hitcount from logdata.accesslog
group by hour
order by hour
Notice that the Query Validator tells you that the query syntax is valid (indicated by the green check mark) and indicates how much data the query will process. The amount of data processed allows you to determine the price of the query using the Cloud Platform Pricing Calculator.

Click Run and examine the results. At what time of day is the website busiest? When is it least busy?

Task 4: Perform a query on the data using the bq command
In this section of the lab, you use the bq command in Cloud Shell to query the accesslog table you created previously.

On the Google Cloud Platform Console, click Activate Cloud Shell Activate Cloud Shell then click Continue.

At the Cloud Shell prompt, enter this command:

bq query "select string_field_10 as request, count(*) as requestcount from logdata.accesslog group by request order by requestcount desc"

The first time you use the bq command, it caches your Google Cloud Platform credentials, and then asks you to choose your default project. Choose the project that Qwiklabs assigned you to. Its name will look like qwiklabs-gcp- followed by a hexadecimal number.

The bq command then performs the action requested on its command line. What URL offered by this web server was most popular? Which was least popular?

Congratulations!
In this lab, you loaded data stored in Cloud Storage into a table hosted by Google BigQuery. You then queried the data to discover patterns.