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
```
    [[AFAppsflyProvider defaultProvider] 
    configureWithAppKey:@"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
    andRepoUrl:@"https://hub.appsfly.io/executor/fetch-build"];
    
```
### Step 4
```
  [[AFAppsflyProvider defaultProvider] syncMicroApps:handles withCompletion:^(NSError * _Nullable error) {
            [[AFMicroAppProvider defaultProvider] presentMicroApp:@"io.appsfly.prateek-dev" OverController:self withIntent:@"INTENT_NAME" andData:@{INTENT_DATA}];
            self.loadButton.enabled = TRUE;
            if (!error) {
              -----
            }
        }];

```



Note: Contact the integrations@appsfly.io for any issues with integration.
