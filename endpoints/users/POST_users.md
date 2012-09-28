# User Resources

    POST `https://:HIVE_NAME.buzzdata.com/api/users`

## Description

Create a user in a given Hive. The user the application is acting on behalf of must be an Admin of the Hive. 

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

`:HIVE_NAME`      = The Hive you wish to act upon. Leave blank for BuzzData.com
`user[username]`  = the new user's username
`user[email]`     = the new user's email address
`user[password]`  = the new user's password

## Return format

A JSON packet with the details of the newly created User. 

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
        "id": "johnsmith", 
        "location": "", 
        "name": null, 
        "url": "https://testhive.buzzdata.com/johnsmith"
        }
    }
