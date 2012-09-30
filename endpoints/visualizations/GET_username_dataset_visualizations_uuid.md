# Visualizaiton Resources

    GET https://:HIVE_NAME.buzzdata.com/:username/:dataset_short_name/visualizations/:UUID

## Description

Retrieve a specific Visualization associated with the dataset under the given UUID. 

## Requires authentication

You must be using a registered oAuth2 client created in your My Applications menu on BuzzData.com

## Parameters

- **:HIVE_NAME** The specific Hive you wish to query - leave empty for BuzzData.com
- **:USENAME** The username you would like to query
- **:DATASET_SHORT_NAME** The shortname of the dataset the visualization is attached to
- **:UUID** The UUID of the Visualization you'd like to access.

## Return format

A JSON packet lisiting the visualizations details of the requested UUID.

## Errors

***

## Example

**Return**

    {
      "visualization"=>{
        "uuid"=>"brqSnkcXOr4OJKcaaN2on1", 
        "created_at"=>"2012-09-30T12:17:23-04:00", 
        "updated_at"=>"2012-09-30T12:17:23-04:00", 
        "visible_to_public"=>false, 
        "engagement_url"=>"/person1/highlights-of-lcbo-study#!/visualizations", 
        "url"=>"http://www.flickr.com/photos/sil3ntp8nd8/5675965697/?f=hp", 
        "thumbnail_url"=>"http://farm6.static.flickr.com/5270/5675965697_aa23c32e55_t.jpg", 
        "domain"=>"flickr.com", 
        "title"=>"Cool Visualization, EH?"
      }
    }
    
