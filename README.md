## Introduction

*A music streaming startup, Sparkify, has grown their user base and song database even more and want to move their data warehouse to a data lake. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.*

*In this project, I am tasked with building an ETL pipeline that extracts their data from S3, processes them using Spark, and loads the data back into S3 as a set of dimensional tables. This will allow their analytics team to continue finding insights into what songs their users are listening to.*

## How to run

*In order to run this project locally*, please create a file `dl.cfg` in the root of this project with the following data:

```
KEY=YOUR_AWS_ACCESS_KEY
SECRET=YOUR_AWS_SECRET_KEY
```

Create an S3 Bucket named `sparkify-dend` where output results will be stored.

Then run the following command:

`python etl.py`

*To run on an Jupyter Notebook powered by an EMR cluster*, import the notebook found in this project.

## Project structure

Files and description:

- **README.md**: explains the project structure and general workflow
- **dl.cfg**: **please generate this file yourself** File with AWS credentials.
- **etl.py**: Extracts songs and log data from S3, transforms it using Spark, and loads the dimensional tables created in parquet format back to S3.


## ETL pipeline

1. Load credentials
2. Read data from S3
    - Song data: `s3://udacity-dend/song_data`
    - Log data: `s3://udacity-dend/log_data`

3. Process data using spark

    Transforms them to create five different tables listed under `Dimension Tables and Fact Table`.
    Each table includes the right columns and data types. Duplicates are addressed where appropriate.

4. Load the processed data back to S3

    Writes the processed data to partitioned parquet files in table directories on S3.

    Each of the five tables are written to parquet files in a separate analytics directory on S3. Each table has its own folder within the directory.

## Source Data
- **Song datasets**: all json files are stored in subdirectories under */song_data*. Example:

```
{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}
```

- **Log datasets**: all json files are stored in subdirectories under *log_data*. Example:

```
{"artist":"Slipknot","auth":"Logged In","firstName":"Aiden","gender":"M","itemInSession":0,"lastName":"Ramirez","length":192.57424,"level":"paid","location":"New York-Newark-Jersey City, NY-NJ-PA","method":"PUT","page":"NextSong","registration":1540283578796.0,"sessionId":19,"song":"Opium Of The People (Album Version)","status":200,"ts":1541639510796,"userAgent":"\"Mozilla\/5.0 (Windows NT 6.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/36.0.1985.143 Safari\/537.36\"","userId":"20"}
```
