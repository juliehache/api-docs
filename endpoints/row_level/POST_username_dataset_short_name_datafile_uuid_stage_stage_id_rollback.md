# Row Level Resources

    POST https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/:DATAFILE_UUID/stage/:STAGE_ID/rollback

## Description

If you make a mistake and stage updates you don't want to commit, you can roll it back safely using this call. 

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- `:HIVE_NAME` = (optional) The name of the hive you are working on, e.g. 'testhive'
- `:USERNAME` = your username: e.g. 'testuser'
- `:DATASET_SHORT_NAME` = the short name (url name) of the dataset you are working with. For example: 'b-list-celebrities'
- `:DATAFILE_UUID` = The UUID of the Datafile you wish to roll back.
- `:STAGE_ID` = The unique stage_id you received when creating your stage.

## Return format

A JSON packet indicating the success or failure of an operation.

## Errors

***

## Example

**Return**

    {"success":"OK"}
