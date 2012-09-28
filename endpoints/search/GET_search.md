# Search the Public BuzzData Hive.

    GET `https://buzzdata.com/api/search?term='bird'`

## Description

Search the public BuzzData.com Hive. 

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

`term` = the string you'd like to search for.

## Return format

A JSON array containing the results of the search.

## Errors

***

## Example

**Return**

    [
    {
        "cloned": false, 
        "id": "bird-populations", 
        "label": "Bird Populations", 
        "type": "Dataset", 
        "url": "/testuser/bird-populations", 
        "value": "Bird Populations"
    }, 
    {
        "id": "birds", 
        "label": "Birds", 
        "type": "Topic", 
        "url": "/topics/birds", 
        "value": "Birds"
    } 
    ]

Note that while in the sample output above there is one of each Dataset, Topic and Users, a search can return many more. The type of result is based on the `type` attribute.
