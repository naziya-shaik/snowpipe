# snowpipe
## What is Snowpipe?

Snowpipe is a cloud-based service provided by Snowflake DB that allows for real-time data ingestion into Snowflake tables. Snowpipe can be used to ingest data from a variety of sources, including Amazon Web Services (AWS) S3 buckets, Azure Data Lake Storage (ADLS) Gen2 accounts, and Google Cloud Storage buckets.

## How to Create a Snowpipe
To create a Snowpipe, you will need to use SQL commands in Snowflake's worksheet or another client tool that can connect to Snowflake. Here is the basic syntax for creating a Snowpipe:

```sql
CREATE PIPE <pipe_name>
    AUTO_INGEST = { TRUE | FALSE }
    AS
    COPY INTO <table_name>
    FROM @<stage_name>/<file_format_name>/
    PATTERN='<file_name_pattern>'
    [ ON_ERROR = 'CONTINUE' | 'ABORT_STATEMENT' | 'ABORT_TRANSACTION' ]
    [ PURGE = TRUE | FALSE ]
    [ MAX_FILE_SIZE = <n> ]
    [ CREDENTIALS = ( <credential_name> ) ]
    [ COMMENT = '<description>' ]
```

The `CREATE PIPE` statement creates a new Snowpipe. You will need to specify a name for the pipe using the `<pipe_name>` parameter.

The `AUTO_INGEST` parameter specifies whether Snowpipe should automatically ingest new data files as they are added to the specified location. If you set `AUTO_INGEST` to `TRUE`, Snowpipe will automatically detect new files and start ingesting them. If you set `AUTO_INGEST` to `FALSE`, you will need to manually start the ingestion process.

The `COPY INTO` statement specifies the table that the ingested data will be loaded into.

The `FROM` clause specifies the location of the data files to be ingested. You will need to specify the name of the external stage where the files are located, as well as the file format of the data files.

The `PATTERN` parameter specifies a file name pattern to match when ingesting data files. You can use this parameter to only ingest files that match a certain pattern.

The `ON_ERROR` parameter specifies what Snowpipe should do if an error occurs during the ingestion process. You can choose to continue ingesting files (`CONTINUE`), abort the current statement (`ABORT_STATEMENT`), or abort the entire transaction (`ABORT_TRANSACTION`).

The `PURGE` parameter specifies whether Snowpipe should delete data files from the external stage after they have been successfully ingested.

The `MAX_FILE_SIZE` parameter specifies the maximum size of data files that Snowpipe should ingest, in bytes.

The `CREDENTIALS` parameter specifies the name of the external stage credential to use when accessing the data files.

The `COMMENT` parameter allows you to add a description to the Snowpipe.
