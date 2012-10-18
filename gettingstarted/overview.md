## Application Registration Overview

1. Create or use an existing BuzzData account on [http://buzzdata.com](http://buzzdata.com)

	![AppMenu](https://raw.github.com/buzzdata/api-docs/master/gettingstarted/images/menu.png)

2. Choose the My Applications option from the main My Profile menu. You will see the BuzzData Applications panel. Click the Register An Application link.

	![RegisterAnApp](https://raw.github.com/buzzdata/api-docs/master/gettingstarted/images/registering_an_app.png)

3. Fill i￼n all of the Application details in the pop up modal box and click Register Application:

	￼**Note**: Application icons should be 205x205 pixels. If you choose not to upload one at this stage you can edit the application later and add an appropriate icon, but a default BuzzData icon will be used until then to represent the Application. 

4. Once your application details have all been completed and the App is registered, its tokens and callback URLs will display in the 'Applications you have registered' section:

	![RegisteredApp](https://raw.github.com/buzzdata/api-docs/master/gettingstarted/images/registered_app.png)
  
	**Note**: BuzzData uses oAuth2 as its authentication mechanism, and should work with any oAuth2 library for the language you care to use. If you have any problems please let us know.

	**Note**: The Application URL should be the URL that initiates the Application  interaction with the user. This URL will be called with the username that the application is to act on behalf of, the origin (app_store, dataroom, datafile), and the dataroom id if the origin is a dataroom, datafile UUID if the origin is a datafile, as query string parameters, ordered alphabetically.  

	**Note**: For testing purposes, you can run an application on localhost and supply  those details in the Application registration and it will work.

5. At this stage your application will appear in the App Store which is at the URL http://buzzdata.com/appstore and in a user’s Datarooms and Datafile as a selectable application. 

	![AppStore](https://raw.github.com/buzzdata/api-docs/master/gettingstarted/images/app_store.png)


## User Application Initiation Flow From App Store

1. A user will select an Application to activate from the App Store at [http://buzzdata.com/appstore](http://buzzdata.com/appstore)
2. A Modal box will appear which allows the user to activate the App on their account.
	
		**NOTE**: The Application will have to handle the instance where the user does not  authorize the Application by ticking the box - in this case the oAuth access token  will be in the invalid_grant state. Once the user authorizes the Application, your Application will be free to make any API calls on behalf of the user and display results in the modal dialogue. 

		**NOTE**: Since the origin at this point will be app-store, your application will not be  passed any details associated with a Dataroom. You should decide what you want to show the user at this point, it could be a list of their datarooms or what  have you.
	
  	**NOTE**: BuzzData tokens will not expire. Future activations by the user will not show the Authorization screen unless the token access is revoked by the user. 
  	
  	**NOTE**: The application should implement a ‘Save’ button that signals that the  user is done manipulating their data and the Application should save the results back to BuzzData.   

3. At this point the Application is authorized on the Users account and will also appear in the list of Applications in their Datarooms and Datafile versions.
￼
The Application activation from the Dataroom is much the same, except that when this happens, the origin parameter will be dataroom, and the Application will be passed the Dataroom short name. The Application should look up the oAuth2 authorization token previously granted in Step 3 with the supplied user name and use it to immediately begin operations with the API as necessary. 

	![DataRoom](https://raw.github.com/buzzdata/api-docs/master/gettingstarted/images/from_dataroom.png)
	
Application activation from a Dataset is achieved by the Applications menu on the Datafile Version:

![Datafile](https://raw.github.com/buzzdata/api-docs/master/gettingstarted/images/form_dataset.png)

**NOTE**: Applications are scoped by Hive. Applications created on BuzzData.com will be available to everyone. Applications created in a Hive will only be available to users of that Hive.

**NOTE**: The application ignition URL will soon contain Hive information along with the username and dataroom shortname, version and datafile UUID as appropriate. 

## Registering Application Output with BuzzData as Visualizations

At the moment, BuzzData supports a flag on the [Create Visualization from URL](https://github.com/buzzdata/api-docs/blob/master/endpoints/visualizations/POST_username_dataset_visualizations_url.md) call that will use [Embed.ly](http://embed.ly/) to generate a preview from the URL by using the [oEmbed protocol](http://www.oembed.com/), and then launch the passed URL inside an iFrame when clicked in the Visualization gallery. So for example, you would make the following BuzzData API call (remember to use an oAuth2 library):

	POST https://:HIVE_NAME.buzzdata.com/:username/:dataset_short_name/visualizations/

With the ```POST``` body containing the ```URL``` parameter that links back to where the Visualization lives, and also the ```APP_RESOURCE``` parameter set to true. 

### Implementing oEmbed in your Application
In order for this to work, your application will have to implement an oEmbed endpoint that can be passed a URL that belongs to your site, and the response should be an oEmbed response containing information about where a preview image can be found, it's dimensions etc. For example:

- Let's say you have an application that makes cool interactive visualizations from data pulled from BuzzData via the API.
- Say your application generates an interactive visualization at ```http://mycoolapp.com/visualizations/johns-visualization```
	- This page should have the link tags mentioned below in its ```HEAD``` tag so that Embedly knows where to make the next call. 
- Your application should implement an endpoint like http://mycoolapp.com/oembed and take a query string parameter of url=http://mycoolapp.com/visualizations/johns-visualization, e.g. ```http://mycoolapp.com/oembed?url=http://mycoolapp.com/visualizations/johns-visualization```
- Your app should be able to dissect the passed URL and lookup the original visualization internally, and return back the following example JSON response:

		{
			"version": "1.0",
			"type": "photo",
			"width": 240,
			"height": 160,
			"title": "Kittens Born in 2012",
			"url": "http://farm4.static.flickr.com/3123/2341623661_7c99f48bbf_m.jpg",
			"author_name": "John McDowall",
			"author_url": "http://mycoolapp.com/users/john/",
			"provider_name": "My Cool App",
			"provider_url": "http://mycoolapp.com/"
		}

- If your application is embedding as a interactive HTML visualization then you should investigate the ```rich``` type and set the width and height to be the optimal viewing size for your application. 
- A thumbnail_url parameter should be passed to an image that represents what the visualization will look like. 

In the above example, because the ```type``` is ```photo``` the expectation is that the ```url``` parameter leads to an image that can be used as a preview thumbnail. If you wanted an embedded HTML fragment that is suitable for a preview, then the ```type``` should be ```rich```. You can find out more by reading the [oEmbed documentation.](http://www.oembed.com/)

### Making your oEmbed endpoint discoverable

You will have to make sure the following link tags are present in your Application's HTML ```HEAD``` tag contents, so that Embedly can know where to call to get the oEmbed JSON fragment it needs:

	<link rel="alternate" type="application/json+oembed"
				href="http://mycoolapp.com/oembed?url=http://mycoolapp.com/visualizations/johns-visualization"
				title="Kittens Born in 2012 oEmbed Profile" />

	<link rel="alternate" type="text/xml+oembed"
		href="http://mycoolapp.com/oembed?url=http://mycoolapp.com/visualizations/johns-visualization"
		title="Kittens Born in 2012 oEmbed Profile" />

### Summary

- Make sure you application pages have the correct ```link``` tags as mentioned above in the ```HEAD``` HTML tag of your pages.
- Implement an oEmbed endpoint that will take a ```url``` query string parameter, look up the resource internally, and respond with a JSON packet as outlined above. 

An additional benefit is that Users can also take the URL of their Visualization from you app and use the BuzzData interface to add it manually, or even embed that output anywhere that understands the oEmbed protocol, like Pinterest for example.



## Appendix A - HMAC Calculations

An [HMAC](http://en.wikipedia.org/wiki/HMAC) signature is also included of all of the parameters in the query string using your Consumer Secret as the Key. This will allow you to take the query string parameters, perform the same HMAC calculation and confirm that the request is legitimate. You can calculate the HMAC by taking the query string parameters in alphabetical order, including the ampersands in the query string like so: 

	hive=buzzdata&origin=app_store&signature=aNT6UwHgmfRnjBFJiQ7D_5J1BIc&user_name=john

Remove the signature query string parameter:

	hive=buzzdata&origin=app_store&user_name=john

Perform a standard HMAC calculation using your consumer secret as the key, and you should end up with the same signature value that was passed to your application in the query string. Example in Ruby:

	# Takes a bunch of hash keys and values, makes a query string out of them and
	# calculates an HMAC value.
	def url_hmac( opts={} )
	  key = [ self.secret ]
	  options = Hash[opts.sort]       			# Sort the incoming Options hash
	  options.delete_if { |k, v| v.nil?  }    	# Delete any nils
	  param_string = options.to_query    	 	# to_query is From ActiveSupport.
	  Base64.urlsafe_encode64(OpenSSL::HMAC.digest(DIGEST, key.pack("H*"),
	              param_string).to_s).gsub!(/=+$/, "") 
	end 