# Data Ingestion to Snowflake from External Stage with Mulesoft

Step:1:
	Create a snowflake account for 30 days.
	Set the role to ACCOUNTADMIN

Step:2
A warehouse in snowflake provides the required resources, such as CPU, memory, and temporary storage, to perform the DML operations.
create warehouse ‘Warehouse_Name’;
create database ‘database_name’
create schema ‘database_name.Schema_name’

Step:3
Execute the below command to create storage object. This object helps you to connect to AWS bucket.
	create or replace storage integration Snow_MUL
	 type = external_stage
	 storage_provider = s3
	  enabled = true
	  storage_aws_role_arn = 'arn role created'
	 storage_allowed_locations = ('s3://bucketName/');

Step:4
The below describe command helps you get the Amazon Resource Names ARN.Amazon Resource Names (ARNs) uniquely identify AWS resources.
	desc integration Snow_MUL;

Step:5
create file format in snowflake

CREATE FILE FORMAT MY_CSV
TYPE = 'CSV'
FIELD_DELIMITER = ','
RECORD_DELIMITER = '\n'
SKIP_HEADER = 1;

Step:6
A stage specifies where data files are stored so that the data in the files can be loaded into a table.

CREATE STAGE my_s3_stage
    URL = 's3://my-snowflake-bucket/data/'
    STORAGE_INTEGRATION = Snow_MUL
    FILE_FORMAT = MY_CSV;


Step:7
Create a target table


Step:8
Use the below copy command to load data in the table.
COPY INTO my_table
FROM @my_s3_stage/my_data.csv
FILE_FORMAT = (TYPE = 'CSV' FIELD_OPTIONALLY_ENCLOSED_BY = '"')
ON_ERROR = 'CONTINUE';


**MuleSoft**

1.Drap and drop copy into connector
2. Provide the connector configuration details

![image](https://github.com/user-attachments/assets/6183bcd2-76af-43da-8874-aa00bdabe304)
![image](https://github.com/user-attachments/assets/7dbdcd7a-1c43-4596-83e2-668cfe670af3)
![image](https://github.com/user-attachments/assets/f0658a3f-5eb9-483d-8ef5-729e4cdeace5)







