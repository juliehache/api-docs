# Dataset Resources

    POST https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/:DATAFILE_UUID/download_request

## Description

Before you can download a dataset, you need to create a `download_request`. Successful requests will return a URL from which to download the data. You can then perform a GET to download the dataset with the returned URL.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- **:HIVE_NAME**          = (optional) The name of the hive you are querying
- **:USERNAME**           = is your username: e.g. 'testuser'
- **:DATASET_SHORT_NAME** = the short name (url name) of the dataset you are downloading. For example: 'b-list-celebrities'
- **:DATAFILE_UUID**      = the unique identifier of the file. This can be seen when you make a "list_datafiles" API call.

**POST Parameters:**

- `version` = the version of the dataset you wish to download

## Return format

A JSON Packet describing the location of the download

## Errors

Note that if you give an invalid version number(a version that does not exist) in the "download_request" command, then the wget call will result in an internal server error:

    HTTP request sent, awaiting response... 500 Internal Server Error
    2012-07-17 11:18:22 ERROR 500: Internal Server Error.

## Example

See an example <a href="https://github.com/buzzdata/buzzdata_client/blob/master/samples/download_data.rb">here</a>.

**Return**

    {
      "download_request": {
          "url": "https://testhive.buzzdata.com:443/ingest/ingest1/download?download_code=7d81647127305f535f370d42622a2f3de1bfcb87"
      }
    }
