# License Resources

    GET https://buzzdata.com/api/licenses

## Description

Retrieve a list of the supported Licenses that a Dataset can be published with. 

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

***

## Return format

A JSON array containing all of the licenses available. 

## Errors

***

## Example

**Return**

    [
      {
          "id": "cc0"
      }, 
      {
          "id": "pdm"
      }, 
      {
          "id": "cc_by"
      }, 
      ...
    ]
