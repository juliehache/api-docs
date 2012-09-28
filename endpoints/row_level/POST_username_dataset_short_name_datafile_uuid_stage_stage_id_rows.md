# Row Level Resources

    POST https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/:DATAFILE_UUID/stage/:STAGE_ID/rows

## Description

You can insert rows to your dataset by making a POST to the above URL.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- `:HIVE_NAME` = (optional) The name of the hive you are working on, e.g. 'testhive'
- `:USERNAME` = your username: e.g. 'testuser'
- `:DATASET_SHORT_NAME` = the short name (url name) of the dataset you want to insert rows into. For example: 'b-list-celebrities'
- `:DATAFILE_UUID` = the unique identifier of the file. This can be seen when you make a "list_datafiles" API call.
- `:STAGE_ID` = the ID you received when you created a `stage` (see above "Creating a stage") 

**POST Parameters**

- `rows` = one or more rows to insert in JSON format. Each row should be an array of string values, for example: `["eviltrout", "male", "Toronto"]`

## Return format

A JSON packet indicating success or failure.

## Errors

***

## Example

See example <a href="https://github.com/buzzdata/buzzdata_client/blob/master/samples/append_data.rb">here</a>.

**Return**

    {"success":"OK"}
