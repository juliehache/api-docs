api-docs
========

The BuzzData API provides programmatic access to BuzzData.

Every user of BuzzData is automatically assigned an API key; there's no need to make a specific request. To get your key, login to BuzzData, hover over the 'My Profile' menu at top left, and click on the 'Settings' option. You will see your API key listed at the bottom of the 'Basic Information' section.

Developers can also take advantage of [BuzzData's Ruby Client Library, whose documentation can be found on Github](https://github.com/buzzdata/buzzdata_client). 

To access the API, you must attach your API key as either a query parameter or post variable in the form of `api_key=YOUR_API_KEY`.

To test if your API key works, copy and paste this URL into your address bar:

    https://buzzdata.com/api/test?api_key=YOUR_API_KEY
  
You should get back a JSON object with your username in it, confirming that the key is yours and has authenticated properly. BuzzData's API returns all results in JSON.

## Rate Limits

The API currently limits the requests you can make against it hourly. We have provided two response headers with each request to the API with Rate Limiting Information. They are returned from every API call.

    X-RateLimit-Limit: 5000
    X-RateLimit-Remaining: 4998

`X-RateLimit-Limit` is your current limit per hour. `X-RateLimit-Remaining` is how many requests you have left. If you need more requests than 5,000/hr, please [contact us](mailto:support@buzzdata.com) and we'll do our best to accommodate you.

[**1. Get the details of a dataset**](#datasetdetails)

[**2. List a user's datasets**](#usersdatasets)

[**3. Retrieve a dataset's data file list**`](#datasetlist)

[**4. Retrieve a dataset's version history**](#history)

[**5. Download a datafile from dataset**](#download)

[**6. Publish a dataset**](#publish_dataset)

[**7. Getting the list of topics**](#topics)

[**8. Getting the list of licenses**](#license)

[**9. Creating a dataset object**](#create_dataset)

[**10. Creating a datafile in a dataset**](#create_datafile)

[**11. Make a data upload request**](#upload_request)

[**12. Upload a file**](#upload_file)

[**13. Clone a dataset**](#clone_dataset)

[**14. Delete a dataset**](#delete_dataset)

[**15. Retrieve user details**](#user_details)

[**16. Search a hive**](#search)

[**17. Create a user**](#create_user)

[**18. Preparing to change a datafile / Create a stage**](#create_stage)

[**19. Inserting rows**](#inserting_rows)

[**20. Updating a row**](#updating_row)

[**21. Deleting a row**](#deleting_row)

[**22. Committing datafile changes**](#commit_stage)

[**23. Rolling back a change**](#rollback_stage)


## 1. <a id="datasetdetails">Get the Details of a Dataset</a>

To retrieve information about a dataset, simply make a GET to:

**GET `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME`**

**URL Parameters**

`:HIVE_NAME` = (optional) The name of the hive you are querying

</n>

`:DATASET_SHORT_NAME` = the short name (url name) of the dataset you are downloading. For example: 'b-list-celebrities'

**GET Parameters**

`api_key` = your API Key (optional but necessary for viewing private datasets.)

</n>
**Example**
`curl -s https://testhive.buzzdata.com/api/testuser/bicycle-counts-and-locations/?api_key=f0742761aaf641783d24c8e7b127f8af84799a4e | python -mjson.tool`

**Returns JSON:**

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

**Ruby API Client**

See example <a href="https://github.com/buzzdata/buzzdata_client/blob/master/samples/dataset_overview.rb">here</a>.

 
## 2. <a id="usersdatasets">List a User's Datasets</a>

You can view a list of any user's datasets with the following query: 

**GET `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/datasets/list`**

**URL Parameters**

`:HIVE_NAME` = (optional) The name of the hive you are querying

</n>

`:USERNAME` = The user name you want to know about. For example: 'testuser'

**GET Parameters**

`api_key` = your API Key  (necessary for viewing private or unpublished datasets)

**Example**
`curl -s https://testhive.buzzdata.com/api/testuser/datasets/list?api_key=f0742761aaf641783d24c8e7b127f8af84799a4e | python -mjson.tool`

</n>

**Returns JSON:**

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


## 3. <a id="datasetlist">Retrieve a Dataset's File List</a>
You can retrieve a list of the data files associated with a Dataset/Dataroom:

**GET `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/list_datafiles`**

**URL Parameters**

`:HIVE_NAME` = (optional) The name of the hive you are querying

</n>

`:USERNAME` = The user name you want to know about. For example: 'testuser'

</n>

`:DATASET_SHORT_NAME` = the short name (url name) of the dataset you are downloading. For example: 'b-list-celebrities'


**GET Parameters:**

`api_key` = your API Key  (optional but necessary for viewing private or unpublished datasets.)

**Example**
`curl -s https://testhive.buzzdata.com/api/testuser/bicycle-counts-and-locations/list_datafiles/?api_key=f0742761aaf641783d24c8e7b127f8af84799a4e | python -mjson.tool`

**Returns JSON**

    [
    {
        "data_file": {
            "created_at": "2012-07-17T15:56:20-04:00", 
            "deleted": false, 
            "has_ingested_data": true, 
            "has_upload": true, 
            "name": "54546_Wilcocks St EB from Spadina Ave to Huron St.xls", 
            "sort_order": 0, 
            "updated_at": "2012-07-17T15:56:31-04:00", 
            "uuid": "b6NQwa0eKr4y37yAyCM7w3", 
            "version": 0
        }
    }, 
    {
        "data_file": {
            "created_at": "2012-07-17T15:56:20-04:00", 
            "deleted": false, 
            "has_ingested_data": true, 
            "has_upload": true, 
            "name": "54545_Wilcocks St WB from Spadina Ave to Huron St.xls", 
            "sort_order": 0, 
            "updated_at": "2012-07-17T15:56:31-04:00", 
            "uuid": "b6NVew0eKr4y37yAyCM7w3", 
            "version": 0
        }
    }, 
    ...
    ]

## 4. <a id="history">Retrieve a Dataset's Version History</a>

To retrieve the version history and release notes of a dataset:

**GET `https://:HIVE_NAME.buzzdata.com/api/data_files/:DATAFILE_UUID/history`**

**URL Parameters**

`:HIVE_NAME` = (optional) The name of the hive you are querying

</n>

`:DATAFILE_UUID` = the unique identifier of the file. This can be seen when you make a "list_datafiles" API call.

**GET Parameters:**

`api_key` = your API Key  (optional but necessary for viewing private or unpublished datasets.)

**Example**
`curl -s https://testhive.buzzdata.com/api/data_files/b6NQwa0eKr4y37yAyCM7w3/history?api_key=f0742761aaf641783d24c8e7b127f8af84799a4e | python -mjson.tool`

</n>

**Returns JSON:**

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

## 5. <a id="download">Download a Datafile from a Dataset</a>

Before you can download a dataset, you need to create a `download_request`. Successful requests will return a URL from which to download the data. You can then perform a GET to download the dataset with the returned URL.

**POST `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/:DATAFILE_UUID/download_request`**

**URL Parameters**

`:HIVE_NAME` = (optional) The name of the hive you are querying

</n>

`:USERNAME` is your username: e.g. 'testuser'

</n>

`:DATASET_SHORT_NAME` = the short name (url name) of the dataset you are downloading. For example: 'b-list-celebrities'

</n>

`:DATAFILE_UUID` = the unique identifier of the file. This can be seen when you make a "list_datafiles" API call.

</n>

**POST Parameters:**

`api_key` = your API key

</n>

`version` = the version of the dataset you wish to download

**Example**
`curl -s -X POST -F "api_key=f0742761aaf641783d24c8e7b127f8af84799a4e" -F "version=0" https://testhive.buzzdata.com/api/testuser/bicycle-counts-and-locations/b6NQwa0eKr4y37yAyCM7w3/download_request | python -mjson.tool`

</n>
**Returns JSON:**

    {
    "download_request": {
        "url": "https://testhive.buzzdata.com:443/ingest/ingest1/download?download_code=7d81647127305f535f370d42622a2f3de1bfcb87"
    }
    }

The URL given is where you can download your data. Here is an example of how you can download the file:
`wget https://testhive.buzzdata.com:443/ingest/ingest1/download?download_code=7d81647127305f535f370d42622a2f3de1bfcb87`

Note that this example will save the file with a strange name:
`download?download_code=7d81647127305f535f370d42622a2f3de1bfcb87`

You will have to rename it with it's original extension in order to open it up:
`mv download?download_code=7d81647127305f535f370d42622a2f3de1bfcb87 foo.xls`

Note that if you give an invalid version number(a version that does not exist) in the "download_request" command, then the wget call will result in an internal server error:

    HTTP request sent, awaiting response... 500 Internal Server Error
    2012-07-17 11:18:22 ERROR 500: Internal Server Error.

**Ruby API Client**

See an example <a href="https://github.com/buzzdata/buzzdata_client/blob/master/samples/download_data.rb">here</a>.


## 6. <a id="publish_dataset">Publishing a Dataset</a>

Publishing datasets involves the following process:

1) (optional) Get a topic ID
 
2) (optional) Get a license
  
3) Create a dataset object (requires a topic ID and license)
  
4) Create a data file on the dataset.

5) Make a data upload request

6) Perform an upload

7) Publish the dataset

See the instructions below to accomplish each of these steps.


## 7. <a id="topics">Getting the List of Topics</a>
To retrieve a list of topics and their ids:

  **GET `https://buzzdata.com/api/topics`**

**Example**

`curl -s https://buzzdata.com/api/topics | python -mjson.tool`

</n>

  **Returns JSON:**

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
    

## 8. <a id="license">Get the List of Licenses</a>
  *Licenses:* When creating a dataset, it is necessary to supply a valid license for the data. You can query the available licenses by:

  **GET `https://buzzdata.com/api/licenses`**

**Example**

`curl -s https://buzzdata.com/api/licenses | python -mjson.tool`

</n>

  **Returns JSON:**

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


## 9. <a id="create_dataset">Create a Dataset Object</a>

Before you can upload data to a dataset, you need to create a dataset object. 

**POST `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/datasets`**

**URL Parameters**

`:HIVE_NAME` is the name of your hive

</n>

`:USERNAME` is your username: e.g. 'testuser'

</n>

**POST Parameters**

`api_key` = your API Key

</n>

`dataset[name]` = the name of the dataset

</n>

`dataset[public]` = (true/false) whether the dataset is public or private

</n>

`dataset[readme]` = the content for "About this Dataset"

</n>

`dataset[license]` = the license the dataset is being offered with. See *Licenses* above.

</n>

`dataset[topics][]` = the ids of the topics associated with this dataset. See *Topics* above.

</n>
**Example**

`curl -s -X POST -F "api_key=f0742761aaf641783d24c8e7b127f8af84799a4e" -F "dataset[name]=Bird Populations" -F "dataset[public]=true" -F "dataset[readme]=Data about bird populations" -F "dataset[license]=cc0" -F "dataset[topics][]=Science" https://testhive.buzzdata.com/api/testuser/datasets | python -mjson.tool`

**Returns JSON**

    {
    "dataset": {
        "articles_count": 0, 
        "attachments_count": 0, 
        "avatar": "https://buzzdata.com/images/avatars/unknown_warrior.png?1341239183", 
        "clones_count": 0, 
        "created_at": "2012-07-17T16:52:34-04:00", 
        "data_updated_at": null, 
        "followers_count": 0, 
        "id": "testuser/bird-populations", 
        "license": "cc0", 
        "name": "Bird Populations", 
        "public": true, 
        "readme": "Data about bird populations", 
        "shortname": "bird-populations", 
        "url": "https://testhive.buzzdata.com/testuser/bird-populations", 
        "username": "testuser", 
        "visualizations_count": 0
    }
    }

...or an error message if the dataset couldn't be created.


## 10. <a id="create_datafile">Creating a Datafile in a Dataset</a>

**POST `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/create_datafile`**

**URL Parameters**

`:HIVE_NAME` = the name of your hive, e.g. 'testhive'

</n>

`:USERNAME` = your username: e.g. 'testuser'

</n>

`:DATASET_SHORT_NAME` = the short name (url name) of the dataset you are downloading. e.g. 'b-list-celebrities'

**POST Parameters**

`api_key` = your API key

</n>

`data_file_name` = The name for your datafile, e.g. 'Quarter 1 2012 financial results'

**Example**

`curl -s -X POST -F "api_key=f0742761aaf641783d24c8e7b127f8af84799a4e" -F "data_file_name=foo.xls" https://testhive.buzzdata.com/api/testuser/bird-populations/create_datafile | python -mjson.tool`

**Returns JSON:**

The UUID of the data file is returned which you should use to reference that specific data file in future calls.

    {
    "datafile_uuid": "cX6Coq0fir4y37yAyCM7w3"
    }


## 11. <a id="upload_request">Make a Data Upload Request</a>

To upload data to the system, you need to make an upload request. An upload request returns the HTTP endpoint your upload should be going to, as well as an `upload_code` you pass along to verify it.

**POST `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/upload_request`**

**URL Parameters**

`:HIVE_NAME` = the name of your hive, e.g. 'testhive'

</n>

`:USERNAME` = your username: e.g. 'testuser'

</n>

`:DATASET_SHORT_NAME` =  the short name (url name) of the dataset you are downloading. e.g. 'b-list-celebrities'

</n>

**POST Parameters**

`api_key` = your API key

</n>

`:datafile_uuid` = the UUID of the data file you want to act on

</n>

**Example**
`curl -s -X POST -F "api_key=f0742761aaf641783d24c8e7b127f8af84799a4e" -F "datafile_uuid=cX6Coq0fir4y37yAyCM7w3" https://testhive.buzzdata.com/api/testuser/bird-populations/upload_request | python -mjson.tool`

**Returns JSON:**

    {
    "upload_request": {
        "upload_code": "34fcdf51ae7baa6ab4da7da1be84a9081ff15d9e", 
        "url": "https://testhive.buzzdata.com:443/ingest/ingest1/ingestfile"
    }
    }

Where:

`upload_code` = a unique token that authenticates your upload

</n>

`url` = the endpoint for where the file should be uploaded

**Ruby API Client**

See an example <a href="https://github.com/buzzdata/buzzdata_client/blob/master/samples/upload_data.rb">here</a>.


## 12. <a id="upload_file">Upload a file</a>

Now you can POST your data file. Send a POST request to the URL returned by your `upload_request`(see above).

*Note: Make sure your POST is a multipart, otherwise the file upload will not work.*

</n>

**POST Parameters**

`api_key` = your API Key

</n>

`upload_code` = the `upload_code` returned in the `upload_request`

</n>

`file` = the file data you are uploading to be ingested

</n>

`release_notes` = the change/release notes for this upload

**Example**
`curl -s -X POST -F "api_key=f0742761aaf641783d24c8e7b127f8af84799a4e" -F "upload_code=f43c21f975aaa78bec2f40de3cb7b7d494d1c125" -F file=@demo.xls https://testhive.buzzdata.com:443/ingest/ingest1/ingestfile | python -mjson.tool`

</n>

**Returns JSON:**

    [
    {
        "job_status_token": "aea22c93-ee4b-4d94-b9f1-e98a72fa9c48", 
        "name": "demo.xls", 
        "size": 76288
    }
    ]

`name` = the filename of the upload.

</n>

`size` = the size of the upload in bytes


## 13. <a id="clone_dataset">Clone a dataset</a>

Cloning has been temporarily disabled. 


## 14. <a id="delete_dataset">Delete a dataset</a>

To delete a dataset, make a DELETE call:

**DELETE `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME`**

</n>

**POST Parameters**

`api_key` = your API Key

</n>

**Example**
`curl -s -X DELETE https://testhive.buzzdata.com/api/testuser/bird-populations?api_key=f0742761aaf641783d24c8e7b127f8af84799a4e | python -mjson.tool`

**Returns JSON:**

    {
    "deleted": true, 
    "id": "testuser/bird-populations"
    }

## 15. <a id="user_details">Retrieve User Details</a>

To retrieve information about a particular BuzzData user, perform the following GET:

**GET `https://:HIVE_NAME.buzzdata.com/api/:USERNAME`**

**URL Parameters**

`:HIVE_NAME` = optional, the name of the hive you are accessing 

</n>

`:USENAME` = the username you would like to query


**GET Parameters**

`api_key` = your API Key  (optional but necessary for querying hives.)

</n>
**Example**
`curl -s https://testhive.buzzdata.com/api/testuser?api_key=f0742761aaf641783d24c8e7b127f8af84799a4e | python -mjson.tool`

**Returns JSON:**

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

## 16. <a id="search">Search a Hive</a>

To search BuzzData, make a GET call:

**GET `https://buzzdata.com/api/search`**

**GET Parameters:**

`term` = the string you'd like to search for* 

</n>

`api_key` = your API Key  (optional but necessary for querying Hives.)

</n>
**Example**
`curl 'https://testhive.buzzdata.com/api/search?api_key=f0742761aaf641783d24c8e7b127f8af84799a4e&term=birds' | python -mjson.tool`

**Returns JSON:**

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


## 17. <a id="create_user">Create a User</a>

To create a user, you need to have admin access.

**POST `https://:HIVE_NAME.buzzdata.com/api/users`**

**URL Parameters**

`:HIVE_NAME` = optional, the name of the hive you are accessing, e.g. 'testhive' 

**POST Parameters**

`api_key` = your API Key

</n>

`user[username]` = the new user's username

</n>

`user[email]` = the new user's email address

</n>

`user[password]` = the new user's password

**Example**
`curl -s -X POST -F "api_key=f0742761aaf641783d24c8e7b127f8af84799a4e" -F "user[username]=johnsmith" -F "user[email]=john@test.com" -F "user[password]=xyz123" https://testhive.buzzdata.com/api/users | python -mjson.tool`

**Returns JSON:**

The JSON is the same as the user details:

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


##<a id='row_level_api'></a>The Row-Level API for Buzzdata

In some cases, it makes more sense to update your data on a row by row basis rather than importing a whole dataset at once.
For example, perhaps you made a GPS application and once an hour want to update it with your location. You could use the 
row level API to insert only the new locations into the dataset.


##Staging your Updates

Before you get started with the Row-Level API you'll have to familiarize yourself with the concept of staging your update.
Every time you upload a dataset to buzzdata, it creates a new version in the history. If you have an application that 
updates the dataset frequently, you would end up with many, many versions that would pollute your dataset's history. To 
get around this, we ask that you stage your updates before commiting them.

You can think of staging as setting aside the data that you want to commit later. You start by creating a stage with a
REST call. Then you add your updates to the stage whenever you want. Once you are ready to create a new version and 
update the dataset, you call commit.

In the GPS example above, a good idea might be to stage a day's worth of updates, and then commit them at the end of the
day. It's up to you to decide when it makes sense for your dataset to be released as a new version!


## 18. <a id="create_stage">Preparing to Change a Datafile / Create a Stage</a>

To create a stage on a data file, make a POST to the following URL. You'll receive an id back that your application should remember.

**POST `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/:DATAFILE_UUID/stage`**

**URL Parameters**
 
`:HIVE_NAME` = (optional) The name of the hive you are working on 

</n>

`:USERNAME` = your username: e.g. 'testuser'

</n>

`:DATASET_SHORT_NAME` = the short name (url name) of the dataset you want to change. For example: 'b-list-celebrities'

</n>

`:DATAFILE_UUID` = the unique identifier of the file. This can be seen when you make a "list_datafiles" API call.


**POST Parameters**

`api_key` = your API Key

**Example**
`curl -s -X POST -F "api_key=f0742761aaf641783d24c8e7b127f8af84799a4e" https://testhive.buzzdata.com/api/testuser/bicycle-counts-and-locations/b6NQwa0eKr4y37yAyCM7w3/stage | python -mjson.tool`

**Returns JSON:**

    {"id": "4f30359d5585d3061a000005"}


## 19. <a id='inserting_rows'>Inserting Rows</a>

You can insert rows to your dataset by making a POST to the following URL:

**POST `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/:DATAFILE_UUID/stage/:STAGE_ID/rows`**

**URL Parameters**

`:HIVE_NAME` = (optional) The name of the hive you are working on, e.g. 'testhive'

</n>

`:USERNAME` = your username: e.g. 'testuser'

</n>

`:DATASET_SHORT_NAME` = the short name (url name) of the dataset you want to insert rows into. For example: 'b-list-celebrities'

</n>

`:DATAFILE_UUID` = the unique identifier of the file. This can be seen when you make a "list_datafiles" API call.

</n>

`:STAGE_ID` = the ID you received when you created a `stage` (see above "Creating a stage") 

**POST Parameters**

`api_key` = your API Key

</n>

`rows` = one or more rows to insert in JSON format. Each row should be an array of string values, for example: `["eviltrout", "male", "Toronto"]`

**Example**
`curl -s -X POST -F "api_key=f0742761aaf641783d24c8e7b127f8af84799a4e" -F "rows=[["1","3","5","9"],["7","8","9","10"]]" https://testhive.buzzdata.com/api/testuser/bicycle-counts-and-locations/b6NQwa0eKr4y37yAyCM7w3/stage/8e3160550b78b68587f2f5c89a145ae9923f78e0/rows | python -mjson.tool`


**Returns JSON:**

    {"success":"OK"}

**Ruby API Client**

See example <a href="https://github.com/buzzdata/buzzdata_client/blob/master/samples/append_data.rb">here</a>.


## 20. <a id='updating_row'>Updating a Row</a>

You can update rows based on the row number. Note that the Row Number starts at 0 for the first row, 1 for the second row, and so on. Note that this call is a PUT and not a POST.

**PUT `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/:DATAFILE_UUID/stage/:STAGE_ID/rows/:ROW_NUMBER`**

**URL Parameters**

`:HIVE_NAME` = (optional) The name of the hive you are working on, e.g. 'testhive'

</n>

`:USERNAME` = your username: e.g. 'testuser'

</n>

`:DATAFILE_UUID` = The UUID of the Datafile you wish to update rows.

</n>

`:STAGE_ID` = The unique stage_id you received when creating your stage.

</n>

`:ROW_NUMBER` = The row you are trying to update

**POST Parameters**

`api_key` = your API Key
</n>

`row` = The new row data in JSON format, for example: `["eviltrout", "male", "Toronto"]`

**Example**
`curl -s -X PUT -F "api_key=f0742761aaf641783d24c8e7b127f8af84799a4e" -F 'row=["1","3","5","9"]' https://testhive.buzzdata.com/api/testuser/bicycle-counts-and-locations/b6NVew0eKr4y37yAyCM7w3/stage/9a28230d364ce9ed87fc6f2ae2cc41fecc2d3ad6/rows/1 | python -mjson.tool`

**Returns JSON:**

    {"success":"OK"}

## 21. <a id='deleting_row'>Deleting a Row</a>

You can update rows based on the row number. Note that the Row Number starts at 0 for the first row, 1 for the second row, and so on.

**DELETE `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/:DATAFILE_UUID/stage/:STAGE_ID/rows/:ROW_NUMBER`**

**URL Parameters**

`:HIVE_NAME` = (optional) The name of the hive you are working on, e.g. 'testhive'

</n>

`:USERNAME` = your username: e.g. 'testuser'

</n>

`:DATAFILE_UUID` = The UUID of the Datafile you wish to delete rows from.

</n>

`:STAGE_ID` = The unique stage_id you received when creating your stage.

</n>

`:ROW_NUMBER` = The row you are trying to update

**POST Parameters**

`api_key` = your API Key

</n>

`row` = The new row data in JSON format, for example: `["eviltrout", "male", "Toronto"]`

**Example**
`curl -s -X DELETE -F "api_key=f0742761aaf641783d24c8e7b127f8af84799a4e" https://testhive.buzzdata.com/api/testuser/bicycle-counts-and-locations/b6NVew0eKr4y37yAyCM7w3/stage/df6f3b652883b08f4ddb0d169d0e141281b4b277/rows/1 | python -mjson.tool`

**Returns JSON:**

    {"success":"OK"}


## 22. <a id='commit_stage'>Committing a Stage</a>

If you are happy with the data you've staged, you can commit it:

**POST `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/:DATAFILE_UUID/stage/:STAGE_ID/commit`**

**URL Parameters**

`:HIVE_NAME` = (optional) The name of the hive you are working on, e.g. 'testhive'

</n>

`:USERNAME` = your username: e.g. 'testuser'

</n>

`:DATASET_SHORT_NAME` = the short name (url name) of the dataset you want to commit to. For example: 'b-list-celebrities'

</n>

`:DATAFILE_UUID` = The UUID of the Datafile you wish to commit to.

</n>

`:STAGE_ID` = The unique stage_id you received when creating your stage.

**POST Parameters**

`api_key` = your API Key

**Example**
`curl -s -X POST -F "api_key=f0742761aaf641783d24c8e7b127f8af84799a4e" https://testhive.buzzdata.com/api/testuser/bicycle-counts-and-locations/b6NQwa0eKr4y37yAyCM7w3/stage/8e3160550b78b68587f2f5c89a145ae9923f78e0/commit | python -mjson.tool`

**Returns JSON**

    {
    "success": "OK", 
    "version": 2
    }


## 23. <a id='rollback_stage'>Rolling Back a Stage</a>

If you make a mistake and stage updates you don't want to commit, you can roll it back safely:

**POST `https://:HIVE_NAME.buzzdata.com/api/:USERNAME/:DATASET_SHORT_NAME/:DATAFILE_UUID/stage/:STAGE_ID/rollback`**

**URL Parameters**

`:HIVE_NAME` = (optional) The name of the hive you are working on, e.g. 'testhive'

</n>

`:USERNAME` = your username: e.g. 'testuser'

</n>

`:DATASET_SHORT_NAME` = the short name (url name) of the dataset you are working with. For example: 'b-list-celebrities'

</n>

`:DATAFILE_UUID` = The UUID of the Datafile you wish to roll back.

</n>

`:STAGE_ID` = The unique stage_id you received when creating your stage.


**POST Parameters**

`api_key` = your API Key

**Example**
`curl -s -X POST -F "api_key=f0742761aaf641783d24c8e7b127f8af84799a4e" https://testhive.buzzdata.com/api/testuser/bicycle-counts-and-locations/b6NVew0eKr4y37yAyCM7w3/stage/2a7913fdb7366ce394975c21dc2051152fe45323/rollback | python -mjson.tool`


**Returns JSON**

    {"success":"OK"}

