# Dataset Resources

    GET https://:HIVE_NAME.buzzdata.com/api/data_files/:DATAFILE_UUID/history

## Description

To retrieve the version history and release notes of a dataset.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- **:HIVE_NAME**      = (optional) The name of the hive you are querying
- **:DATAFILE_UUID**  = the unique identifier of the file. This can be seen when you make a "list_datafiles" API call.


## Return format

A JSON array contaoning the information about the versions of the Dataset.

## Errors

***

## Example

**Return**

    [
    {
        "avatar": "https://buzzdata.com/images/avatars/unknown_warrior.png?1341239183", 
        "created_at": 1342556356, 
        "release_notes": "Latest data.", 
        "username": "testuser", 
        "version": 1
    }, 
    {
        "avatar": "https://buzzdata.com/images/avatars/unknown_warrior.png?1341239183", 
        "created_at": 1342554988, 
        "release_notes": "", 
        "username": "testuser", 
        "version": 0
    }
    ]
