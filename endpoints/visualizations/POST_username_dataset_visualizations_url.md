# Visualization Resources

    POST https://:HIVE_NAME.buzzdata.com/api/:username/:dataset_short_name/visualizations/url/

## Description

Create a Visualizaiton from a URL.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- **:HIVE_NAME** The specific Hive you wish to query - leave empty for BuzzData.com
- **:USENAME** The username you would like to query
- **:DATASET_SHORT_NAME** The shortname of the dataset the visualization is attached to

** POST Parameters

- **:URL** The URL of the visualization you wish to create. 
- **:APP_RESOURCE** [true, false] Indicate that this visualization is the result of an Application. (optional, defaults to false)

## Return format

A JSON packet indicating the success of the operation.

## Errors

***

## Example

**Return**

      { 'success': 'ok' }
    
