# Dataset Resources

    POST https://:HIVE_NAME.buzzdata.com/api/:USERNAME/datasets

## Description

Create a Dataset object to allow the uploading and publishing of Datafiles.

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- `:HIVE_NAME` is the name of your hive
- `:USERNAME` is your username: e.g. 'testuser'
- `dataset[name]`     = the name of the dataset
- `dataset[public]`   = (true/false) whether the dataset is public or private
- `dataset[readme]`   = the content for "About this Dataset"
- `dataset[license]`  = the license the dataset is being offered with. See *Licenses* above.
- `dataset[topics][]` = the ids of the topics associated with this dataset. See *Topics* above.

## Return format

A JSON packet containing the information about the newly created Dataset.

## Errors

***

## Example

**Return**

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
