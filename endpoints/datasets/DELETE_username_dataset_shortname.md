# Dataset Resources

    DELETE https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME

## Description

Delete a Dataset.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- :HIVE_NAME
- :USERNAME
- :DATASET_SHORT_NAME

## Return format

A JSON packet confirming the deletion details of the deleted dataset.

## Errors

***

## Example

**Return**

    {
      "deleted": true, 
      "id": "testuser/bird-populations"
    }
