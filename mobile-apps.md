<staging>---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-18"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Adding {{site.data.keyword.appid_short}} to your mobile apps
{: #adding-mobile}

Using {{site.data.keyword.appid_short}}, you can quickly construct an authentication layer for your native or hybrid mobile application.

## Understanding the flow
{: #understanding}

**When would this flow be useful?**

When you are developing a desktop or mobile phone application that will be installed on a user's device (a native application), you can use the {{site.data.keyword.appid_short}} mobile flow to obtain user identity information. Using this flow, you can securely authenticate users on your app in order to provide personalized user experiences across devices.

**What is the flow's technical basis?**

Since native applications are installed directly on a user's device, private user information and application credentials can be extracted by third-parties with relative ease. By default, these types of applications are known as untrusted clients as they cannot store global credentials or user refresh tokens. As a result, untrusted clients require users to input their credentials every time their access tokens expire.

In order to convert your application into a trusted client, {{site.data.keyword.appid_short}} leverages [Dynamic Client Registration](https://tools.ietf.org/html/rfc7591). Before your application begins authenticating users, each application instance registers as an OAuth2 client with {{site.data.keyword.appid_short}}. As a result of client registration, your app receives an installation-specific client ID and secret converting it into a confidential client. This process minimizes your app's risk of exposing credentials indefinitely and greatly improve the user experience by allowing automatic token refresh.

Following registration, your users authenticate using either the OAuth2 `authorization code` or `resource owner password` [authorization grant](https://tools.ietf.org/html/rfc6749#section-1.3) flows to authenticate users.

**What does this flow look like?**

![{{site.data.keyword.appid_short_notm}} app to app flow](./images/mobile-auth-flow.png)

Dynamic Client Registration

1. A user performs an action that triggers a request by the client application to the {{site.data.keyword.appid_short}} SDK.
2. If your app has not yet registered as a mobile client, the SDK initiates a dynamic registration flow.
3. On a successful registration, {{site.data.keyword.appid_short}} returns your installation specific client ID and secret.

Authorization Flow

<ol start="4">
  <li>The {{site.data.keyword.appid_short}} SDK starts the authorization process using the {{site.data.keyword.appid_short_notm}} `/authorization` endpoint.</li>
  <li>The login widget is displayed to the user.</li>
  <li>The user authenticates using one of the configured identity providers.</li>
  <li>{{site.data.keyword.appid_short}} returns an authorization grant.</li>
  <li>The authorization grant is exchanged for access, identity, and refresh tokens from the {{site.data.keyword.appid_short_notm}} `/token` endpoint.</li>
</ol>

## Configuring your mobile app with the {{site.data.keyword.appid_short}} SDKs
{: #configuring}

Get started with {{site.data.keyword.appid_short}} using our SDKs.
{: shortdesc}

### Before you begin
{: #before-installation}

You will need the following information:

  1. An {{site.data.keyword.appid_short_notm}} instance

  2. Your instance's tenant ID. This can be found in the **Service Credentials** tab of your service dashboard.

  3. Your instance's deployment {{site.data.keyword.Bluemix}} region. You can find your region by looking at the console.

    <table><caption> Table 1. {{site.data.keyword.Bluemix_notm}} regions and corresponding SDK values</caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} Region</th>
      <th>SDK value</th>
    </tr>
    <tr>
      <td>US South</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY</code></td>
    </tr>
    <tr>
      <td>United Kingdom</td>
      <td><code>AppID.REGION_UK</code></td>
    </tr>
    <tr>
      <td>Germany</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

## Authentication with the Android SDK
{: #android-setup}

**Requirements**

{: #requirements-android}

  * API 27 or above
  * Java 8.x
  * Android SDK Tools 26.1.1+
  * Android SDK Platform Tools 27.0.1+
  * Android Build Tools version 27.0.0+

**Installing the SDK**

{: #install-android}

1. Create an Android Studio project or open an existing project.

2. Add the JitPack repository to your root `build.gradle` file.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. Find your application's `build.gradle` file.

    **Note**: Be sure to open the file for your app, not the project `build.gradle` file.

    Add the {{site.data.keyword.appid_short_notm}} client SDK to the dependencies section of

    ```gradle
    dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
    }
    ```
    {: codeblock}

    In the `defaultConfig` section, configure the redirect scheme.

    ```gradle
    defaultConfig {
      ...
      manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
    }
    ```
    {: codeblock}

6. Synchronize your project with Gradle. Click **Tools > Android > Sync Project with Gradle Files**.

**Initializing the SDK**

{: #initialize-android}

1. Pass the context, tenant ID, and region parameters to the initialize method to configure the SDK.

    A common, though not mandatory, place to put the initialization code is in the onCreate method of the main activity in your Android application.
    {: tip}

    ```java
    AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <region>);
    ```
    {: codeblock}

</br>

**Starting the Authorization Flow**

{: #start-android}

1. Define an AuthorizationListener to handle authentication flow events.

    ```java
    AuthorizationListener listener = new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
            //Exception occurred
        }

        @Override
        public void onAuthorizationCanceled () {
            //Authentication canceled by the user
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            //User authenticated
        }
    });
    ```

2. Start an authorization flow using the LoginWidget.

    ```java
    AppID.getInstance().getLoginWidget().launch(this, listener);
    ```

Check out our other documentation to learn more about [managing the user sign-in](/docs/services/appid/login-widget.html#default) experience!
{: tip}

Now, you're ready to configure your identity providers and start authenticating users! For more information on the Android SDK, see the <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="blank">{{site.data.keyword.appid_short_notm}} Android GitHub repository<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

## Authentication with the iOS Swift SDK
{: #ios-setup}

Protect your mobile applications using the {{site.data.keyword.appid_short}} client SDK.
{:shortdesc}


**Requirements**

{: #requiements-ios}

  * Xcode 9.0 or above
  * CocoaPods 1.1.0 or higher
  * iOS 10.0 or higher

**Installing the SDK**

{: #install-ios}

The {{site.data.keyword.appid_short_notm}} client SDK is distributed with CocoaPods, a dependency manager for Swift and Objective-C Cocoa projects. CocoaPods downloads artifacts, and makes them available to your project.

1. Create an Xcode project or open an existing one.

2. Create a new or open your existing `Podfile` in the project's directory.

3. Add the `IBMCloudAppID` pod and `use_frameworks!` command to your target's dependencies

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID'
  end
  ```
  {: codeblock}

4. Install your dependencies from the command line within your project directory.

  ```swift
  $ pod install --repo-update
  ```
  {: codeblock}

5. After installation, open the `<your app>.xcworkspace` file containing your Xcode project and your linked dependencies

6. Enable keychain sharing in your Xcode project. Navigate to **Project Settings > Capabilities > Keychain Sharing** and select **Enable keychain sharing**.

7. Open **Project Settings > Info > URL Types**, and add a **URL Type**. Place the following value in both the **Identifier** and the **URL Scheme** text boxes.
  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}


**Initializing the SDK**

{: #initialize-ios}

1. Initialize the client SDK by passing the tenant ID and region parameters to the initialize method.

    A common, though not mandatory, place to put the initialization code is in the `application:didFinishLaunchingWithOptions` method of the AppDelegate in your Swift application.
    {: tip}

    ```swift
      AppID.sharedInstance.initialize(tenantId: <tenantId>, region: <region>)
    ```
    {: codeblock}

2. Import the {{site.data.keyword.appid_short}} SDK to your `AppDelegate` file.

    ```swift
    import IBMCloudAppID
    ```
    {: codeblock}

3. Configure your application to process redirects through {{site.data.keyword.appid_short}}.

  ```swift
  func application(application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey: Any]) -> Bool {
      return AppID.sharedInstance.application(application, open: url, options: options)
  }
  ```
  {: codeblock}

</br>

**Starting the Authorization Flow**

{: #start-ios}

1. Create an AuthorizationDelegate class in your application

    ```swift
    class Delegate: AuthorizationDelegate {
        public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
            //User authenticated
        }

        public func onAuthorizationCanceled() {
            //Authentication canceled by the user
        }

        public func onAuthorizationFailure(error: AuthorizationError) {
            //Exception occurred
        }
    }
    ```

2. Launch the login widget from your controller.

    ```swift
    AppID.sharedInstance.loginWidget?.launch(delegate: Delegate())
    ```

Check out our other documentation to learn more about [managing the user sign-in](/docs/services/appid/login-widget.html#default) experience!
{: tip}

Now you're ready to configure your identity providers and start authenticating users! For more information about the iOS SDK, see the <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="blank">{{site.data.keyword.appid_short_notm}} iOS GitHub repository <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

## Accessing protected APIs
{: #accessing-protected-apis}

After a successful login flow, you can use your access and identity tokens to invoke protected backend resources using the SDK or a networking library of your choice.

### Swift SDK

1.  Add the following imports to the file in which you want to invoke a protected resource request:

    ```swift
    import BMSCore
    import IBMCloudAppID
    ```

2. Invoke your protected resource

     ```swift
    BMSClient.sharedInstance.initialize(region: <region>)
    BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)

    let request =  Request(url: "<your protected resource url>")

    request.send { (response: Response?, error: Error?) in

        guard let response = response, error == null else {
            print("An error occurred invoking a protected resources", error?.localizedDescription ?? "No response was received")
            return;
        }
        // use your response object
    })
    ```

### Android SDK

1. Add the following imports to the file in which you want to invoke a protected resource request:

    ```java
    import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
    import com.ibm.cloud.appid.android.api.AppIDAuthorizationManager;
    ```

2. Invoke your protected resource

     ```java
     BMSClient bmsClient = BMSClient.getInstance();
     bmsClient.initialize(getApplicationContext(), <region>);

     AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
     bmsClient.setAuthorizationManager(appIdAuthMgr);

     Request request = new Request("<your protected resource url>", Request.GET);
     request.send(this, new ResponseListener() {

     @Override
     public void onSuccess (Response response) {
         Log.d("My app", "onSuccess :: " + response.getResponseText());
     }

     @Override
     public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
         if (null != t) {
             Log.d("My app", "onFailure :: " + t.getMessage());
         } else if (null != extendedInfo) {
             Log.d("My app", "onFailure :: " + extendedInfo.toString());
         } else {
             Log.d("My app", "onFailure :: " + response.getResponseText());
             }
         }
     });
    ```

### Invoking protected APIs without the SDK

Using the library of your choice, set your `Authorization` request header to use the `Bearer` authentication scheme to transmit the access token.

Example request format:

```
GET /resource HTTP/1.1
Host: server.example.com
Authorization: Bearer <access token> <optional identity token>
```