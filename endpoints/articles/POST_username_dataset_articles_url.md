# Article Resources

    POST https://:HIVE_NAME.buzzdata.com/:username/:dataset_short_name/articles/

## Description

Create an Article on a given Dataset.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- **:HIVE_NAME** The specific Hive you wish to query - leave empty for BuzzData.com
- **:USENAME** The username you would like to query
- **:DATASET_SHORT_NAME** The shortname of the dataset the article is attached to

** POST Parameters

- **:URL** The URL of the article you wish to create. 

## Return format

A JSON packet indicating the success of the operation.

## Errors

***

## Example

**Return**

      { 'success': 'ok' }
    
