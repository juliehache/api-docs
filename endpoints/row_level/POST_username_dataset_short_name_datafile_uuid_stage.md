# Row Level Resources

    POST https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/:DATAFILE_UUID/stage

## Description

To create a stage on a data file, make a POST to the following URL. You'll receive an id back that your application should remember.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- `:HIVE_NAME` = (optional) The name of the hive you are working on 
- `:USERNAME` = your username: e.g. 'testuser'
- `:DATASET_SHORT_NAME` = the short name (url name) of the dataset you want to change. For example: 'b-list-celebrities'
- `:DATAFILE_UUID` = the unique identifier of the file. This can be seen when you make a "list_datafiles" API call.


## Return format

A JSON packet containg the Stage ID.

## Errors

***

## Example

**Return**

    {"id": "4f30359d5585d3061a000005"}
