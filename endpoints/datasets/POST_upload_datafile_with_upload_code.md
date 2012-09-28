# Dataset Resources

    POST <upload_destination_url>

## Description

Send a POST request to the URL returned by your `upload_request`(see above).

*Note: Make sure your POST is a multipart, otherwise the file upload will not work.*

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- `upload_code` = the `upload_code` returned in the `upload_request`
- `file` = the file data you are uploading to be ingested
- `release_notes` = the change/release notes for this upload

## Return format

***

## Errors

***

## Example

**Return**

    [
    {
          "job_status_token": "aea22c93-ee4b-4d94-b9f1-e98a72fa9c48", 
          "name": "demo.xls", 
          "size": 76288
      }
    ]

- `name` = the filename of the upload.
- `size` = the size of the upload in bytes
