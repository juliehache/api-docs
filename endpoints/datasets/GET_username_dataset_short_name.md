# Dataset Resources

    GET https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME

## Description

Retrieve the information about a Dataset. 

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- **:HIVE_NAME** = (optional) The name of the hive you are querying
- **:DATASET_SHORT_NAME** = the short name (url name) of the dataset you are downloading. For example: 'b-list-celebrities'

## Return format

A JSON packet containing the information about the Dataset.

## Errors

***

## Example

See example <a href="https://github.com/buzzdata/buzzdata_client/blob/master/samples/dataset_overview.rb">here</a>.

**Return**

    {
    "dataset": {
        "articles_count": 0, 
        "attachments_count": 0, 
        "avatar": "https://buzzdata.com/images/avatars/unknown_warrior.png?1341239183", 
        "clones_count": 0, 
        "created_at": "2012-07-17T15:55:48-04:00", 
        "data_updated_at": "2012-07-17T15:56:29-04:00", 
        "followers_count": 0, 
        "id": "testuser/bicycle-counts-and-locations", 
        "license": null, 
        "name": "Bicycle Counts and Locations", 
        "public": false, 
        "readme": "Number of bikes at given intersections at given times at given locations throughout the city.", 
        "shortname": "bicycle-counts-and-locations", 
        "url": "https://testhive.buzzdata.com/testuser/bicycle-counts-and-locations", 
        "username": "testuser", 
        "visualizations_count": 0
    }}
