# Visualization Resources

    POST https://:HIVE_NAME.buzzdata.com/api/:username/:dataset_short_name/visualizations/image/

## Description

POST an image you wish to user as a visualization.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- **:HIVE_NAME** The specific Hive you wish to query - leave empty for BuzzData.com
- **:USENAME** The username you would like to query
- **:DATASET_SHORT_NAME** The shortname of the dataset the article is attached to

** POST Parameters

- **:IMAGE** The MultiPart POST image you wish to use

## Return format

A JSON packet indicating the success of the operation.

## Errors

***

## Example

**Return**

      { 'success': 'ok' }
    
