# User Resources

    DELETE https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/:DATAFILE_UUID/stage/:STAGE_ID/rows/:ROW_NUMBER

## Description

You can update rows based on the row number. Note that the Row Number starts at 0 for the first row, 1 for the second row, and so on.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- `:HIVE_NAME` = (optional) The name of the hive you are working on, e.g. 'testhive'
- `:USERNAME` = your username: e.g. 'testuser'
- `:DATAFILE_UUID` = The UUID of the Datafile you wish to delete rows from.
- `:STAGE_ID` = The unique stage_id you received when creating your stage.
- `:ROW_NUMBER` = The row you are trying to update

**POST Parameters**

- `row` = The new row data in JSON format, for example: `["eviltrout", "male", "Toronto"]`

## Return format

A JSON packet indicating success or failure of the operation.

## Errors

***

## Example

**Return**

    {"success":"OK"}
