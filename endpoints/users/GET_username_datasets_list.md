# User Resources

    GET https://:HIVE_NAME.buzzdata.com/api/:USERNAME/datasets/list

## Description

Returns a list of any user's public datasets.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- **:HIVE_NAME** _(optional)_ — The name of the Hive the user belongs to, or nothing to reference BuzzData.com
- **:USERNAME** — The username you wish to query.

## Return format

A JSON Array containing the public Datasets. 

## Errors

***

## Example

**Return**

    [
      {
        "id": "testuser/bicycle-counts-and-locations", 
        "name": "Bicycle Counts and Locations", 
        "public": false, 
        "readme": "Number of bikes at given intersections at given times at given locations throughout the city.", 
        "url": "https://testhive.buzzdata.com/testuser/bicycle-counts-and-locations"
      },
      ...
    ]