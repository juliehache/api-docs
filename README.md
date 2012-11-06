BuzzData API
============

The BuzzData API allows you to access functionality and data programatically via oAuth2 secured API calls. 

**NOTE: This documentation covers the new version of the API that will be released soon. If you want access to this
    please contact [support@buzzdata.com](mailto:support@buzzdata.com) to request access.**

If you are looking for the documentation for the current public API on buzzdata.com, head to the [FAQ](http://buzzdata.com/faq/api).

## Pre-requisites

- In order to use the API, you must be able to use an oAuth2 library in the language of your choice.
- All API calls should be made over SSL connections.
- Your application server must **not** send the header `X-Frame-Origin: DENY`, or `X-Frame-Origin: SAMEORIGIN` as this will prevent the 
Application from being loaded inside an iFrame by the Browser. You should use the `X-Frame-Origin: ALLOW-FROM buzzdata.com` header, which you can
read more about [here](http://blogs.msdn.com/b/ieinternals/archive/2010/03/30/combating-clickjacking-with-x-frame-options.aspx). Please contact
[support@buzzdata.com](mailto:support@buzzdata.com) if you have any queries about this flag.

## Getting Started

BuzzData's API is [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) based and uses basic HTTP communication with JSON responses. The API is only available to registered client applications, but it's easy to create one. You can follow the [getting started guide](https://github.com/buzzdata/api-docs/blob/master/gettingstarted/overview.md). 

## Rate Limits

The API currently limits the requests you can make against it hourly. We have provided two response headers with each request to the API with Rate Limiting Information. They are returned from every API call.

    X-RateLimit-Limit: 5000
    X-RateLimit-Remaining: 4998

`X-RateLimit-Limit` is your current limit per hour. `X-RateLimit-Remaining` is how many requests you have left. If you need more requests than 5,000/hr, please [contact us](mailto:support@buzzdata.com) and we'll do our best to accommodate you.

## Client Libraries

- [Ruby](https://github.com/buzzdata/buzzdata_client)

## Endpoints

#### Users

- **[<code>GET</code> :username](https://github.com/buzzdata/api-docs/blob/master/endpoints/users/GET_username.md)** - Get the details of a User.
- **[<code>GET</code> :username/datasets/list](https://github.com/buzzdata/api-docs/blob/master/endpoints/users/GET_username_datasets_list.md)** - Get the datasets a user has.
- **[<code>POST</code> users](https://github.com/buzzdata/api-docs/blob/master/endpoints/users/POST_users.md)** - Create a new user.

#### Licenses

- **[<code>GET</code> licenses](https://github.com/buzzdata/api-docs/blob/master/endpoints/licenses/GET_licenses.md)** - Get a list of Licenses available.

#### Topics

- **[<code>GET</code> topics](https://github.com/buzzdata/api-docs/blob/master/endpoints/topics/GET_topics.md)** - Get a list of topics available. 

#### Search

- **[<code>GET</code> search](https://github.com/buzzdata/api-docs/blob/master/endpoints/search/GET_search.md)** - Search the public buzzdata.com site.

#### Datasets
Datasets are the overall container for Datafiles, Articles, Visualizations etc.

- **[Overview](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/overview.md)**
- **[<code>POST</code> :username/datasets](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/POST_username_datasets.md)** - Create a Dataset object to allow the uploading and publishing of Datafiles.
- **[<code>POST</code> :username/:dataset_short_name/upload_request](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/POST_username_dataset_short_name_upload_request.md)** - Upload a new Datafile to a Dataroom. 
- **[<code>GET</code> data_files/:DATAFILE_UUID/history](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/GET_data_files_datafile_uuid_history.md)** - To retrieve the version history and release notes of a dataset.
- **[<code>GET</code> :username/:dataset_short_name](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/GET_username_dataset_short_name.md)** - Retrieve the information about a Dataset.
- **[<code>GET</code> :username/:dataset_short_name/list_datafiles](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/GET_username_dataset_short_name_list_datafiles.md)** - Retrieves a list of Datafiles associated with a Dataset/Dataroom.
- **[<code>POST</code> upload_url](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/POST_upload_datafile_with_upload_code.md)** - Send a POST request to the URL returned by your `upload_request`
- **[<code>POST</code> :username/:dataset_short_name/:datafile_uuid/download_request](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/POST_username_dataset_short_name_datafile_uuid_download_request.md)** - Create a `download_request`
- **[<code>DELETE</code> :username/:dataset_short_name](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/DELETE_username_dataset_shortname.md)** - Delete a Dataset.

#### Datafiles
Datafiles are the actual files associated with a Dataroom that contain data, or are a document of interest. 

- **[<code>POST</code> :username/:dataset_short_name](https://github.com/buzzdata/api-docs/blob/master/endpoints/datafiles/POST_username_dataset_short_name_create_datafile.md)** - Creates a Datafile within a Dataset.

#### Articles
Articles are the image tiles represented in BuzzData when you visit a Dataset's Articles tab.

- **[<code>DELETE</code> :username/:dataset_short_name/articles/:uuid](https://github.com/buzzdata/api-docs/blob/master/endpoints/articles/DELETE_username_dataset_articles_uuid.md)** - Delete the corresponding article with the given UUID.
- **[<code>GET</code> :username/:dataset_short_name/articles](https://github.com/buzzdata/api-docs/blob/master/endpoints/articles/GET_username_dataset_articles.md)** - Retrieve a list of the Articles associated with the dataset.
- **[<code>GET</code> :username/:dataset_short_name/articles/:uuid](https://github.com/buzzdata/api-docs/blob/master/endpoints/articles/GET_username_dataset_articles_uuid.md)** - Retrieve a given Article associated with the dataset.
- **[<code>POST</code> :username/:dataset_short_name/articles](https://github.com/buzzdata/api-docs/blob/master/endpoints/articles/POST_username_dataset_articles_url.md)** - Create an Article on a given Dataset.

#### Visualizations
Visualizations are the image tiles represented in BuzzData when you visit a Dataset's Visualizations tab.

- **[<code>DELETE</code> :username/:dataset_short_name/visualizations/:uuid](https://github.com/buzzdata/api-docs/blob/master/endpoints/visualizations/DELETE_username_dataset_visualization_uuid.md)** - Delete the corresponding visualization with the given UUID.
- **[<code>GET</code> :username/:dataset_short_name/visualizations](https://github.com/buzzdata/api-docs/blob/master/endpoints/visualizations/GET_username_dataset_visualizations.md)** - Retrieve a list of the Visualizations associated with the dataset.
- **[<code>GET</code> :username/:dataset_short_name/visualizations/:uuid](https://github.com/buzzdata/api-docs/blob/master/endpoints/visualizations/GET_username_dataset_visualizations_uuid.md)** - Retrieve a specific Visualization associated with the dataset under the given UUID.
- **[<code>POST</code> :username/:dataset_short_name/visualizations](https://github.com/buzzdata/api-docs/blob/master/endpoints/visualizations/POST_username_dataset_visualizations_url.md)** - Create a Visualizaiton from a URL.
- **[<code>POST</code> :username/:dataset_short_name/visualizations](https://github.com/buzzdata/api-docs/blob/master/endpoints/visualizations/POST_username_dataset_visualizations_image.md)** - POST an image you wish to user as a visualization.

#### Row Level Dataset Access
The Row Level Dataset Access allows you to add or remove rows from datasets by creating stages. 

- **[Overview](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/overview.md)**
- **[<code>DELETE</code> :username/:dataset_short_name/:datafile_uuid/stage/:stage_id](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/DELETE_username_dataset_short_name_datafile_uuid_stage_stage_id_rows_row_number.md)** - Delete a row
- **[<code>POST</code> :username/:dataset_short_name/:datafile_uuid/stage](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/POST_username_dataset_short_name_datafile_uuid_stage.md)** - To create a stage on a data file
- **[<code>POST</code> :username/:dataset_short_name/:datafile_uuid/stage/:stage_id/commit](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/POST_username_dataset_short_name_datafile_uuid_stage_stage_id_commit.md)** - To commit a stage
- **[<code>POST</code> :username/:dataset_short_name/:datafile_uuid/stage/:stage_id/rollback](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/POST_username_dataset_short_name_datafile_uuid_stage_stage_id_rollback.md)** - To rollback a stage you don't want to commit
- **[<code>POST</code> :username/:dataset_short_name/:datafile_uuid/stage/:stage_id/rows](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/POST_username_dataset_short_name_datafile_uuid_stage_stage_id_rows.md)** - Insert one or more rows via a Stage
- **[<code>PUT</code> :username/:dataset_short_name/:datafile_uuid/stage/:stage_id/rows/:row_number](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/PUT_username_dataset_short_name_datafile_uuid_stage_stage_id_rows_row_number.md)** - Update rows based on row number.

