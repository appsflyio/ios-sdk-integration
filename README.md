# How to integrate the Appsfly Ios Utils

### Step 1
#### Add Cocoapods:
Add the following to the pod file.

```
pod 'AFSDK'
```
### Step 2
#### Install the pod by running below command
```
pod install
```

### Step 3
#### Generated Secret-key

Obtain a unique secret key from Appsfly.io (xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx). To keep the secret key secure, it is recommended to follow the below steps.

1. Place this code in the Appdelegate file of the Ios Project.

    '[[AFAppsflyProvider defaultProvider] configureWithAppKey:@"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" andRepoUrl:@"https://hub.appsfly.io/executor/fetch-build"];'


### Step 3

#### Initialize runtime with MicroApp configurations

Override your Application/Activity Instance onCreate() method 

```
@Override
public void onCreate() {
	super.onCreate();

	ArrayList<AppsFlyClientConfig> appsFlyClientConfigs = new ArrayList<AppsFlyClientConfig>();
	AppsFlyClientConfig appsflyConfig = new AppsFlyClientConfig(context, "MICRO_MODULE_HANDLE", "EXECUTION_URL");
	appsFlyClientConfigs.add(appsflyConfig);
	AppsFlyProvider.getInstance().initialize(appsFlyClientConfigs, this);
}
```
This will start the process of syncing Metadata required to run MicroApp in your application.

### Step 4

#### Fly in MicroApp into context of user

To launch the MicroApp, run the following snippet where there is a call to action.

```
MicroAppLauncher.pushApp(*MICRO_MODULE_HANDLE*, *INTENT*, *new JSONObject(){INTENT_DATA}*, *ACTIVITY*);
```

___

# Data into and out of MicroApp

### To put data into the MicroApp:
```
//Put context data inside a JSONobject and pass it as intent data.
JSONObject contextData = new JSONObject();
data.put(*key* , *value*);
MicroAppLauncher.pushApp(*MICRO_MODULE_HANDLE*, *INTENT*, data, *ACTIVITY*);
```

> Note: Values and format accepted by the Microapp are specific to each Microapp and can be found in the respective Microapp documentation.

### To retrieve data from the MicroApp:
```
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	super.onActivityResult(requestCode, resultCode, data);
	if (resultCode == RESULT_OK && requestCode == AppsFlyConstants.NAVIGATION_CODE) {
		    String dataStr = data.getStringExtra("postData");
		    JSONObject resultData;
		    try {
			resultData = new JSONObject(dataStr);
		    } catch (JSONException e) {
			e.printStackTrace();
		    }
		    //Get values from resultData with keys specified by the Microapp Documentation.
		    Object value1 = resultData.get(*key1*);
		    String value2 = resultData.getString(*key2*);
	}
}
```

> Note: Values returned by the Microapp are specific to each Microapp and can be found in the respective Microapp documentation.

___


Note: Contact the integrations@appsfly.io for any issues with integration.
