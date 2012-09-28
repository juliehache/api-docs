# Dataset Resources

    POST https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/upload_request

## Description

Upload a new Datafile to a Dataroom. To upload data to the system, you need to make an upload request. An upload request returns the HTTP endpoint your upload should be going to, as well as an `upload_code` you pass along to verify it.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- `:HIVE_NAME` = the name of your hive, e.g. 'testhive'
- `:USERNAME` = your username: e.g. 'testuser'
- `:DATASET_SHORT_NAME` =  the short name (url name) of the dataset you are downloading. e.g. 'b-list-celebrities'

**POST Parameters**

- `:datafile_uuid` = the UUID of the data file you want to act on

## Return format

Returns JSON with the Upload code and destination URL to use. 

## Errors

***

## Example

See an example <a href="https://github.com/buzzdata/buzzdata_client/blob/master/samples/upload_data.rb">here</a>.

**Return**

    {
      "upload_request": {
          "upload_code": "34fcdf51ae7baa6ab4da7da1be84a9081ff15d9e", 
          "url": "https://testhive.buzzdata.com:443/ingest/ingest1/ingestfile"
      }
    }
