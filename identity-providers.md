---

copyright:
  years: 2017
lastupdated: "2017-09-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Configuring identity providers
{: #setting-up-idp}

You can configure Facebook, Google, or a combination of the two to set up a single sign-on experience for your users. By using an identity provider, users are able to sign in with credentials they are already familiar with.

{:shortdesc}


## Configuring Facebook authentication
{: #facebook}

Configure the {{site.data.keyword.appid_short}} service to use Facebook as an identity provider.


### Getting an app ID and secret from Facebook
{: #getting-facebook-appid}

To use Facebook as an identity provider on your mobile or web apps, you must add and configure the website platform on your Facebook application.

1. Log in to your account on the <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for Developers site <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
2. Make note of the Facebook app ID and secret. These values are needed to configure your web project for authentication in your service dashboard.
3. Add the web platform and enter the site URL.
4. From the products list, select **Facebook Login**.
5. In the Valid OAuth redirect URLs field, enter the authorization server callback endpoint URL. After configuring your service instance, you can add this value.
6. Click **Save Changes**.

### Configuring {{site.data.keyword.appid_short_notm}} for Facebook authentication
{: #configuring-facebook-appid}

When you have your Facebook app ID and secret, and your Facebook for Developers app is configured to serve web clients, you can edit the Facebook authentication in your service dashboard.

1. From the **Manage** tab of your service dashboard, select **Facebook** and click **Edit**.
2. Enter the Facebook app ID and secret that you obtained from the Facebook for Developers website.
3. Copy the URI that is in the **Redirect URI for Facebook for Developers** field. Paste the URI into the **Valid OAuth redirect URIs** field in the **Facebook Login** section of the Facebook Developers Portal.
4. Click **Save**.
5. Optional: For web apps, enter the redirect URL in the **Web Application Redirect URLs** field. This value is determined by the developer and used to access the redirect URL after the authorization process is completed.


## Configuring Google authentication
{: #google}

Configure the {{site.data.keyword.appid_short_notm}} service to use Google as an identity provider.


### Getting a client ID and secret from Google
{: #google-client-id}

To use Google as an identity provider, obtain a Google client ID and secret and create a project in the Google Developer Console.

1. Open your Google application in the <a href="https://console.developers.google.com/apis/library" target="_blank">Google Developer Console <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
2. Add the Google+ API.
3. Create credentials by using OAuth. In the **Application Type** field, select **Web application**. In the **Authorized redirect URIs** field, enter the {{site.data.keyword.appid_short_notm}} redirect URI. You can obtain the {{site.data.keyword.appid_short_notm}} redirect authorization URI from the Google configuration screen of the service dashboard.
4. Make note of the Google client ID and secret and save your changes.



### Configuring {{site.data.keyword.appid_short_notm}} for Google authentication
{: #google-client-appid}

When you have your Google client and secret, and your Google Developers console is configured to serve web clients, you can edit the Google authentication in your service dashboard.

1. From the **Manage** tab of your service dashboard, select **Google** and click **Edit**.
3. Enter the Google Client ID and Secret that you obtained from the Google Developers console.
4. Copy the URI that is in the **Redirect URI for Google for Developers** field. Paste the URI into the **Authorized redirect URIs** field that is under **Restrictions** in the **Client ID for web application** section of the Google Developers Portal.
5. Click **Save**.
6. Optional: For web apps, enter the redirect URI in the **Web Application Redirect URIs** field. This value is determined by the developer and used to access the redirect URI after the authorization process completes.
