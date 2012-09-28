# Datafile Resources

    POST `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/create_datafile`**

## Description

Creates a Datafile within a Dataset. 

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- **:HIVE_NAME**          = the name of your hive, e.g. 'testhive'
- **:USERNAME**           = your username: e.g. 'testuser'
- **:DATASET_SHORT_NAME** = the short name (url name) of the dataset you are downloading. e.g. 'b-list-celebrities'

**POST Parameters**

- `data_file_name` = The name for your datafile, e.g. 'Quarter 1 2012 financial results'

## Return format

The UUID of the data file is returned which you should use to reference that specific data file in future calls.

## Errors

***

## Example

**Return**

    {
      "datafile_uuid": "cX6Coq0fir4y37yAyCM7w3"
    }
