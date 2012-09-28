# User Resources

    GET `https://:HIVE_NAME.buzzdata.com/api/:USERNAME`

## Description

To retrieve information about a particular BuzzData user.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- **:HIVE_NAME** The specific Hive you wish to query - leave empty for BuzzData.com
- **:USENAME** The username you would like to query

## Return format

JSON describing the User details. 

## Errors

***

## Example

**Return**

    {
    "user": {
        "avatar": "https://buzzdata.com/images/avatars/unknown_warrior.png?1341239183", 
        "datasets_count": 0, 
        "description": "", 
        "followers_count": 0, 
        "id": "testuser", 
        "location": "", 
        "name": null, 
        "url": "https://testhive.buzzdata.com/testuser"
        }
    }
