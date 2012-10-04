## Application Registration Overview

1. Create or use an existing BuzzData account on [http://buzzdata.com](http://buzzdata.com)

	![AppMenu](https://raw.github.com/buzzdata/api-docs/master/gettingstarted/images/menu.png)

2. Choose the My Applications option from the main My Profile menu. You will see the BuzzData Applications panel. Click the Register An Application link.

	![RegisterAnApp](https://raw.github.com/buzzdata/api-docs/master/gettingstarted/images/registering_an_app.png)

3. Fill i￼n all of the Application details in the pop up modal box and click Register Application:

	￼**Note**: Application icons should be 205x205 pixels. If you choose not to upload   one at this stage you can edit the application later and add an appropriate icon, but a default BuzzData icon will be used until then to represent the Application. 

4. Once your application details have all been completed and the App is registered, its tokens and callback URLs will display in the 'Applications you have registered' section:

	![RegisteredApp](https://raw.github.com/buzzdata/api-docs/master/gettingstarted/images/registered_app.png)
  
	**Note**: BuzzData uses oAuth2 as its authentication mechanism, and should work with any oAuth2 library for the language you care to use. If you have any problems please let us know.

	**Note**: The Application URL should be the URL that initiates the Application  interaction with the user. This URL will be called with the logged in username, the   origin (app_store, dataroom, datafile), and the dataroom short name if the origin   is a dataroom, datafile UUID if the origin is a datafile, as query string parameters,   ordered alphabetically.  

	**Note**: For testing purposes, you can run an application on localhost and supply  those details in the Application registration and it will work.

5. At this stage your application will appear in the App Store which is at the URL http://buzzdata.com/appstore and in a user’s Datarooms and Datafile as a selectable application. 

	![AppStore](https://raw.github.com/buzzdata/api-docs/master/gettingstarted/images/app_store.png)


## User Application Initiation Flow From App Store

1. A user will select an Application to activate from the App Store at [http://buzzdata.com/appstore](http://buzzdata.com/appstore)
2. ￼A Modal box will appear which allows the user to activate the App on their account.
	
	**NOTE**: The Application will have to handle the instance where the user does not  authorize the Application by ticking the box - in this case the oAuth access token  will be in the invalid_grant state. Once the user authorizes the Application, your Application will be free to make any API calls on behalf of the user and display results in the modal dialogue. 

	**NOTE**: Since the origin at this point will be app-store, your application will not be  passed any details associated with a Dataroom. You should decide what you   want to show the user at this point, it could be a list of their datarooms or what  have you.
	
  	**NOTE**: The Application should store the oAuth2 authorization token associated  with the user name so that future activations do not require re-authorization of  the application. This will work as BuzzData tokens will not expire. 
  	
  	**NOTE**: The application should implement a ‘Save’ button that signals that the  user is done manipulating their data and the Application should save the results  back to BuzzData.   

3. At this point the Application is authorized on the Users account and will also appear in the list of Applications in their Datarooms and Datafile versions.
￼
The Application activation from the Dataroom is much the same, except that when this happens, the origin parameter will be dataroom, and the Application will be passed the Dataroom short name. The Application should look up the oAuth2 authorization token previously granted in Step 3 with the supplied user name and use it to immediately begin operations with the API as necessary. 

	![DataRoom](https://raw.github.com/buzzdata/api-docs/master/gettingstarted/images/from_dataroom.png)
	
Application activation from a Dataset is achieved by the Applications menu on the Datafile Version:

![Datafile](https://raw.github.com/buzzdata/api-docs/master/gettingstarted/images/form_dataset.png)

**NOTE**: Applications are scoped by Hive. Applications created on BuzzData.com will be available to everyone. Applications created in a Hive will only be available to users of that Hive.

**NOTE**: The application ignition URL will soon contain Hive information along with the username and dataroom shortname, version and datafile UUID as appropriate. 

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