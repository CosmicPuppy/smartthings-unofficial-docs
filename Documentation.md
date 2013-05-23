
# SmartThings

## JSON API Endpoints

First off, you need to be logged into http://graph.api.smarthings.com … Which is simple enough. You can then go on to see a list of your hubs and events, among other things, in their dashboard. However, we're after JSON responses and all of hte data you see here is available in (seemingly open) JSON responses.

For the purposes of the following example responses, note that  `<idHashString>` values represent 32 character long alpha-numeric unique IDs. You will see other placeholder values as well, but the `<idHashString>` values will be useful to make other API calls. You will see another hash string placeholder value `<uuid>` which is a normal [UUID](http://en.wikipedia.org/wiki/Universally_unique_identifier).

### Authenticating
Before you can make any of these HTTP requests you will need to be logged in. You can do that manually as explained above, but you can also with code using oauth.

Remember, every call that you will be making will display data relative to the account you are logged in with. You will not have permission to view certain data and you certainly can't get information about other accounts. 

### Accounts
Get information about your accounts.    
[https://graph.api.smartthings.com/api/accounts](https://graph.api.smartthings.com/api/accounts)

Example response:

	[
		{
			id: "<idHashString>",
			name: "<email>'s Account",
			fullName: "<yourName>",
			locked: false,
			permissions: "a"
		}
	]

### Account Details
You'll want to replace "idHashString" here in the URL with your account ID string found in the **Accounts** endpoint or **Locations** endpoint. This call will return a combination of some of the data found in some of the other endpoints. It will include your account, locations, and recent events.    
[https://graph.api.smartthings.com/api/accounts/idHashString](https://graph.api.smartthings.com/api/accounts/idHashString)

### Account Locations
Get information about locations for a specific account. Replace "idHashString" with your account ID string found in the **Accounts** endpoint or **Locations** endpoint.    
[https://graph.api.smartthings.com/api/accounts/idHashString/locations](https://graph.api.smartthings.com/api/accounts/idHashString/locations)

### Account Events
Get the recent events for an account. Replace "idHashString" with your account ID string found in the **Accounts** endpoint or **Locations** endpoint.    
[https://graph.api.smartthings.com/api/accounts/idHashString/events](https://graph.api.smartthings.com/api/accounts/idHashString/events)

Example response:

	[
		{
			id: "<uuid>",
			hubId: "<idHashString>",
			description: "SmartSense Motion detected motion has stopped",
			displayed: true,
			linkText: "SmartSense Motion",
			date: "2013-05-22T23:20:04.126Z",
			unixTime: 1369264804126,
			value: "inactive",
			deviceId: "<idHashString>",
			name: "motion",
			locationId: "<idHashString>"
		},
		{
			id: "<uuid>",
			hubId: "<idHashString>",
			description: "SmartSense Motion detected motion",
			displayed: true,
			linkText: "SmartSense Motion",
			date: "2013-05-22T23:19:02.291Z",
			unixTime: 1369264742291,
			value: "active",
			deviceId: "<idHashString>",
			name: "motion",
			locationId: "<idHashString>"
		},
		...
	]

### Hubs
Get information about your connected hubs.    
[https://graph.api.smartthings.com/api/hubs](https://graph.api.smartthings.com/api/hubs)

Example response:

	[
		{
			id: "<idHashString>",
			name: "My House",
			locationId: "<idHashString>",
			firmwareVersion: "000.009.00004",
			zigbeeId: "<idString>",
			status: "ACTIVE",
			onlineSince: "2013-05-22T22:00:44.858Z",
			signalStrength: null,
			batteryLevel: null,
			type: {
				name: "Hub"
			},
			virtual: false,
			permissions: "a"
		}
	]

### Hub Details
Get information about your hub, the connected devices, and recent events. The ten latest events appear to be displayed.    
[https://graph.api.smartthings.com/api/hubs/idHashString](https://graph.api.smartthings.com/api/hubs/idHashString)

Example response:

	{
		account: {
			id: "<idHashString>",
			name: "<email>'s Account",
			fullName: "<yourName>",
			locked: false,
			permissions: "a"
		},
		locations: [
			{
				id: "<idHashString>",
				name: "Old apt",
				accountId: "<idHashString>",
				latitude: "",
				longitude: "",
				regionRadius: 50,
				backgroundImage: "https://smartthings-location-images.s3.amazonaws.com/standard/standard51.jpg",
				mode: {
					id: "<idHashString>",
					name: "Home"
				},
				modes: [
					{
						id: "<idHashString>",
						name: "Away"
					},
					{
						id: "<idHashString>",
						name: "Home"
					},
					{
						id: "<idHashString>",
						name: "Night"
					}
				],
				permissions: "a"
			}
		],
		events: [
			{
				id: "<uuid>",
				hubId: "<idHashString>",
				description: "SmartSense Motion detected motion has stopped",
				displayed: true,
				linkText: "SmartSense Motion",
				date: "2013-05-23T00:11:10.900Z",
				unixTime: 1369267870900,
				value: "inactive",
				deviceId: "<idHashString>",
				name: "motion",
				locationId: "<idHashString>"
			},
			…
		]
	}

### Hub Events
Get the last few (currently 10) events for a hub.    
[https://graph.api.smartthings.com/api/hubs/idHashString/events](https://graph.api.smartthings.com/api/hubs/idHashString/events)

*Note: The response looks just like the account events endpoint response.*

### All Locations
Get information about your locations for all accounts.    
[https://graph.api.smartthings.com/api/locations](https://graph.api.smartthings.com/api/locations)

Example response:

	[
		{
			id: "<idHashString>",
			name: "<yourLocationName>",
			accountId: "<idHashString>",
			latitude: "",
			longitude: "",
			regionRadius: 50,
			backgroundImage: "https://smartthings-location-images.s3.amazonaws.com/standard/standard51.jpg",
			mode: {
				id: "<idHashString>",
				name: "Home"
			},
			modes: [
				{
					id: "<idHashString>",
					name: "Away"
				},
				{
					id: "<idHashString>",
					name: "Home"
				},
				{
					id: "<idHashString>",
					name: "Night"
				}
			],
			permissions: "a"
		}
	]
	
### List All SmartApps
Note: This endpoint will take a little while to load because the response is quite large. It has nothing to do with your hub or account. What it does is it lists all of the available SmartApps that have been created.

It tells you things like the current version of the SmartApp, it's install count, etc. It is essentially an app catalog and it's interesting to browse through it since it contains titles and descriptions for each app. Interestingly enough some of these applications don't even have anything to do with your sensors - though they appear to notify you just the same.

*Note: This call does not require authentication.*    
[https://graph.api.smartthings.com/api/smartapps/](https://graph.api.smartthings.com/api/smartapps/)

### SmartApp Details
This will return information about a particular SmartApp, using its ID which can be found from the above call (or the next call).

*Note: This call does not require authentication.*      
[https://graph.api.smartthings.com/api/smartapps/idHashString](https://graph.api.smartthings.com/api/smartapps/idHashString)

	{
		id: "8a9c25843e38742c013e4e1498ea26b6",
		version: 0.9,
		state: "LATEST_APPROVED",
		name: "Alfred Workflow",
		description: "This SmartApp allows you to interact with the things in your physical graph through Alfred.",
		iconUrl: "https://s3.amazonaws.com/smartapp-icons/Partner/alfred-app.png",
		iconX2Url: "https://s3.amazonaws.com/smartapp-icons/Partner/alfred-app@2x.png",
		dateCreated: "2013-04-28T00:39:32Z",
		lastUpdated: "2013-05-09T14:43:36Z",
		preferences: {
			sections: [
				{
					title: "Allow Alfred to Control These Things...",
					input: [
					{
						title: "Which Switches?",
						description: "Tap to set",
						multiple: true,
						required: false,
						name: "switches",
						type: "capability.switch"
					},
					{
						title: "Which Locks?",
						description: "Tap to set",
						multiple: true,
						required: false,
						name: "locks",
						type: "capability.lock"
					}
					]
				}
			]
		},
		installedCount: 32,
		author: "SmartThings",
		photoUrls: [ ],
		videoUrls: [ ],
		smartApp: {
			id: "8a9c25843e38742c013e4e1498ea26b6"
		},
		mostRecentVersionId: "8a9c25843e38742c013e4e14f1b226b8"
	}

### Your SmartApp Installations
On the otherhand, this endpoint will tell you about the applications you have installed. This call will return some of the same information found in the above SmartApps details call but also contains some information specific to your account. It will include information such as `eventSubscriptions`, location information, and other preferences specifically set by you when you installed/configured the SmartApp.    
[https://graph.api.smartthings.com/api/smartapps/installations/](https://graph.api.smartthings.com/api/smartapps/installations/)

