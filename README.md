---
services: active-directory-b2c
platforms: ios
author: parakhj
---

# Integrate Azure AD B2C into an Objective-C iOS application using ROPC

**This sample demonstrates how to use Azure AD B2C using a 3rd party library called AppAuth. It has only been tested for compatibility in basic scenarios with Azure AD B2C. Issues and feature requests related to AppAuth should be directed to the library's open-source project.**

This sample is a quickstart to help you get started with Azure AD B2C on iOS using a 3rd party library called AppAuth. The focus of this sample is to show you how you can *natively build a sign-in experience* within your app while using Azure AD B2C. **This sample uses an authorization flow called Resource Owner Password Credential (ROPC).** Unless an absolute requirement, we do not recommend using this flow. You should use the authorization code flow, which is demonstrated in this [sample](https://github.com/Azure-Samples/active-directory-b2c-ios-native-appauth).

This sample was created by following the README instructions from the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS). For more details on how the sample and the library work, please reference the AppAuth README on GitHub.

## Steps to Run

Follow the instructions below to configure the sample for your Azure AD B2C configuration. To use Azure AD B2C, you'll first need to create an Azure AD B2C tenant, register your application, and create a "Resource owner policy".

* To create an Azure AD B2C tenant, checkout [these steps](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-get-started).

* To register your app, checkout [these steps](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-app-registration).  Make sure the "Native Client" switch is turned to "Yes".  You will need to supply a Redirect URL with a custom scheme in order for your iOS application to capture the callback.  To avoid a collision with another application, we recommend using a reverse DNS notation of your B2C tenant name followed by your application name as the custom scheme.  The example Redirect URI in this sample is: `com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect` where fabrikamb2c should be replaced with your tenant name, and exampleapp should be replaced with the name of your application.

* Create a Resource Owner Policy.

* Clone the code

### Install the libary

1. Open terminal, and navigate to `Examples/Example-iOS_ObjC/`folder.

2. Run the following command to install the AppAuth pod.

```
pod install
```

### Setting up the iOS App

1. In Finder, navigate to `Examples/Example-iOS_ObjC/` and open `Example-iOS_ObjC.xcodeproj`. This will open the project in XCode.

2. Open `AppAuthExampleViewController.m`, replace the following fields:

    * `kIssuer`: Should be `https://login.microsoftonline.com/tfp/{Tenant Name}.onmicrosoft.com/{Signup or Signin Policy Name}/v2.0` (This is not necessary for ROPC. This sample allows both experiences in one app)
    * `kIssuerROPC`: Should be `https://login.microsoftonline.com/tfp/{tenantName}.onmicrosoft.com/{Resource Owner Policy Name}/v2.0`
    * `kClientId`: This is your Application ID, which can be found in the Azure Portal (under Application settings).
    * `kRedirectUri`: This is your redirect URI, which can be found in the Azure Portal (under Application settings).

3. Scroll down, and update:
    * `username`: Replace 'demob2cuser@outlook.com' with the user that you would like to sign in.
    * `password`: Insert the user's password here.
    * `scope`: The value for the scope parameter in the request.

4. Open Info.pList.  Expand 'URL types' -> 'Item 0' -> 'URL Schemes' -> 'Item 0'.  Update the scheme 'msalb35a3d9b' to match the scheme of the kRedirectUri value updated in ViewController.m.

5. Go ahead and try the app. Upon completing the login process, you should see the types of tokens acquired.


## Questions & Issues

Please file any questions or problems with the sample as a github issue.  You can also post on Stackoverflow with the tag `azure-ad-b2c`.

This sample was built and tested with the iOS 10.2 Simulator on XCode 9.1.  

## Acknowledgements

This sample was created using instructions from the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).

## Contributing

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.