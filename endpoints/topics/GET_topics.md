# Topics Resources

    GET https://buzzdata.com/api/topics

## Description

Retrieve a list of all of the topics on BuzzData.com

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

***

## Return format

Returns a JSON array of all of the topics and their IDs.

## Errors

***

## Example

**Return**

    [
    {
        "id": "agriculture", 
        "name": "Agriculture"
    }, 
    {
        "id": "animals", 
        "name": "Animals"
    }, 
    {
        "id": "anthropology", 
        "name": "Anthropology"
    }, 
    ...
    ]
