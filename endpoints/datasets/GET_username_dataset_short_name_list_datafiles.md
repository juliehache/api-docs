# Dataset Resources

    GET https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/list_datafiles

## Description

Retrieves a list of Datafiles associated with a Dataset/Dataroom.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- **:HIVE_NAME**          = (optional) The name of the hive you are querying
- **:USERNAME**           = The user name you want to know about. For example: 'testuser'
- **:DATASET_SHORT_NAME** = the short name (url name) of the dataset you are downloading. For example: 'b-list-celebrities'

## Return format

A JSON arracy containing the details about the datafiles.

## Errors

***

## Example

**Return**

    [
    {
        "data_file": {
            "created_at": "2012-07-17T15:56:20-04:00", 
            "deleted": false, 
            "has_ingested_data": true, 
            "has_upload": true, 
            "name": "54546_Wilcocks St EB from Spadina Ave to Huron St.xls", 
            "sort_order": 0, 
            "updated_at": "2012-07-17T15:56:31-04:00", 
            "uuid": "b6NQwa0eKr4y37yAyCM7w3", 
            "version": 0
        }
    }, 
    {
        "data_file": {
            "created_at": "2012-07-17T15:56:20-04:00", 
            "deleted": false, 
            "has_ingested_data": true, 
            "has_upload": true, 
            "name": "54545_Wilcocks St WB from Spadina Ave to Huron St.xls", 
            "sort_order": 0, 
            "updated_at": "2012-07-17T15:56:31-04:00", 
            "uuid": "b6NVew0eKr4y37yAyCM7w3", 
            "version": 0
        }
    }, 
    ...
    ]
