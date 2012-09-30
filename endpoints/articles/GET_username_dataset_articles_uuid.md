# Article Resources

    GET https://:HIVE_NAME.buzzdata.com/:username/:dataset_short_name/articles/:uuid

## Description

Retrieve a given Article associated with the dataset. 

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- **:HIVE_NAME** The specific Hive you wish to query - leave empty for BuzzData.com
- **:USENAME** The username you would like to query
- **:DATASET_SHORT_NAME** The shortname of the dataset the article is attached to
- **:UUID** The UUID of the article you wish to access.

## Return format

A JSON packet containing details of the articles associated with the UUID.

## Errors

***

## Example

**Return**

      {"article"=>{
        "created_at"=>"2012-09-30T11:47:09-04:00", 
        "engagement_url"=>"/person1/highlights-of-lcbo-study#!/articles", 
        "engagements"=>0, 
        "id"=>256, 
        "payload"=>"{\"url\":\"http://www.nytimes.com/2011/06/06/world/asia/06gates.html?_r=1&hp\",\"thumbnail_url\":\"http://graphics8.nytimes.com/images/2011/06/06/world/06gates-span/06gates-span-articleLarge.jpg\",\"title\":\"Steeper Pullout Is Raised as Option for Afghanistan\",\"domain\":\"nytimes.com\"}", 
        "updated_at"=>"2012-09-30T11:47:09-04:00", 
        "user_id"=>381, 
        "uuid"=>"aylfW8cXyr4OJKcaaN2on1", 
        "visible_to_public"=>false}
      }
    
