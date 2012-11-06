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

- **[<code>GET</code> :username](https://github.com/buzzdata/api-docs/blob/master/endpoints/users/GET_username.md)**
- **[<code>GET</code> :username/datasets/list](https://github.com/buzzdata/api-docs/blob/master/endpoints/users/GET_username_datasets_list.md)**
- **[<code>POST</code> users](https://github.com/buzzdata/api-docs/blob/master/endpoints/users/POST_users.md)**

#### Licenses

- **[<code>GET</code> licenses](https://github.com/buzzdata/api-docs/blob/master/endpoints/licenses/GET_licenses.md)**

#### Topics

- **[<code>GET</code> topics](https://github.com/buzzdata/api-docs/blob/master/endpoints/topics/GET_topics.md)**

#### Search

- **[<code>GET</code> search](https://github.com/buzzdata/api-docs/blob/master/endpoints/search/GET_search.md)**

#### Datasets

- **[Overview](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/overview.md)**
- **[<code>POST</code> :username/datasets](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/POST_username_datasets.md)**
- **[<code>POST</code> :username/:dataset_short_name/upload_request](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/POST_username_dataset_short_name_upload_request.md)**
- **[<code>GET</code> data_files/:DATAFILE_UUID/history](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/GET_data_files_datafile_uuid_history.md)**
- **[<code>GET</code> :username/:dataset_short_name](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/GET_username_dataset_short_name.md)**
- **[<code>GET</code> :username/:dataset_short_name/list_datafiles](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/GET_username_dataset_short_name_list_datafiles.md)**
- **[<code>POST</code> upload_url](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/POST_upload_datafile_with_upload_code.md)**
- **[<code>POST</code> :username/:dataset_short_name/:datafile_uuid/download_request](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/POST_username_dataset_short_name_datafile_uuid_download_request.md)**
- **[<code>DELETE</code> :username/:dataset_short_name](https://github.com/buzzdata/api-docs/blob/master/endpoints/datasets/DELETE_username_dataset_shortname.md)**

#### Datafiles

- **[<code>POST</code> :username/:dataset_short_name](https://github.com/buzzdata/api-docs/blob/master/endpoints/datafiles/POST_username_dataset_short_name_create_datafile.md)**

#### Articles

- **[<code>DELETE</code> :username/:dataset_short_name/articles/:uuid](https://github.com/buzzdata/api-docs/blob/master/endpoints/articles/DELETE_username_dataset_articles_uuid.md)**
- **[<code>GET</code> :username/:dataset_short_name/articles](https://github.com/buzzdata/api-docs/blob/master/endpoints/articles/GET_username_dataset_articles.md)**
- **[<code>GET</code> :username/:dataset_short_name/articles/:uuid](https://github.com/buzzdata/api-docs/blob/master/endpoints/articles/GET_username_dataset_articles_uuid.md)**
- **[<code>POST</code> :username/:dataset_short_name/articles](https://github.com/buzzdata/api-docs/blob/master/endpoints/articles/POST_username_dataset_articles_url.md)**

#### Visualizations

- **[<code>DELETE</code> :username/:dataset_short_name/visualizations/:uuid](https://github.com/buzzdata/api-docs/blob/master/endpoints/visualizations/DELETE_username_dataset_visualization_uuid.md)**
- **[<code>GET</code> :username/:dataset_short_name/visualizations](https://github.com/buzzdata/api-docs/blob/master/endpoints/visualizations/GET_username_dataset_visualizations.md)**
- **[<code>GET</code> :username/:dataset_short_name/visualizations/:uuid](https://github.com/buzzdata/api-docs/blob/master/endpoints/visualizations/GET_username_dataset_visualizations_uuid.md)**
- **[<code>POST</code> :username/:dataset_short_name/visualizations](https://github.com/buzzdata/api-docs/blob/master/endpoints/visualizations/POST_username_dataset_visualizations_url.md)**
- **[<code>POST</code> :username/:dataset_short_name/visualizations](https://github.com/buzzdata/api-docs/blob/master/endpoints/visualizations/POST_username_dataset_visualizations_image.md)**

#### Row Level Dataset Access

- **[Overview](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/overview.md)**
- **[<code>DELETE</code> :username/:dataset_short_name/:datafile_uuid/stage/:stage_id](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/POST_username_dataset_short_name_datafile_uuid_stage_stage_id.md)**
- **[<code>POST</code> :username/:dataset_short_name/:datafile_uuid/stage](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/POST_username_dataset_short_name_datafile_uuid_stage.md)**
- **[<code>POST</code> :username/:dataset_short_name/:datafile_uuid/stage/:stage_id/commit](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/POST_username_dataset_short_name_datafile_uuid_stage_stage_id_commit.md)**
- **[<code>POST</code> :username/:dataset_short_name/:datafile_uuid/stage/:stage_id/rollback](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/POST_username_dataset_short_name_datafile_uuid_stage_stage_id_rollback.md)**
- **[<code>POST</code> :username/:dataset_short_name/:datafile_uuid/stage/:stage_id/rows](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/POST_username_dataset_short_name_datafile_uuid_stage_stage_id_rows.md)**
- **[<code>PUT</code> :username/:dataset_short_name/:datafile_uuid/stage/:stage_id/rows/:row_number](https://github.com/buzzdata/api-docs/blob/master/endpoints/row_level/PUT_username_dataset_short_name_datafile_uuid_stage_stage_id_rows_row_number.md)**

