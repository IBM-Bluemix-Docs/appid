---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Getting started tutorial
{: #gettingstarted}

{{site.data.keyword.appid_full}} helps you to add authentication to your mobile and web apps and protects your back-end resources.
{: shortdesc}

## Creating a service instance
{: #create}

Create an instance of {{site.data.keyword.appid_short_notm}} to get started.
{: shortdesc}

1. In the {{site.data.keyword.Bluemix}} catalog, select {{site.data.keyword.appid_short_notm}}. The service configuration screen opens.
2. Give your service instance a name, or use the preset name.
3. To bind your instance, select an app from the **Connect to** menu. If you select **Leave unbound**, you can bind the service instance later.
4. Select your pricing plan and click **Create**.

## Configuring a sample app
{: #sample-app}

You can use one of the preconfigured sample apps to get familiar with working with the service.
{: shortdesc}

Out of the box, the sample apps are configured with two identity providers and the ability to review authentication. You can also use the login widget feature to customize a sign-in page and see how quickly the updates that you make are shown in your app.

To configure a sample app from the GUI:

1. After you've created instance of the service, you can choose a sample app in a language in which you feel comfortable working. You can choose from iOS Swift, Android, Node.js, and Java. Don't want to use an SDK? Check out our blog on <a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">using {{site.data.keyword.appid_short_notm}} with other languages, such as Python <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
2. Follow the steps in the GUI to **Build and Run** your sample app. Each language is configured slightly differently, so be sure to select the language of the app that you downloaded from the drop-down. Once your app is configured, you can open it in a browser and login by using your credentials.
  **Note**: Ensure that you have the prerequisites installed for the language with which you want to work.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> Android API 25 or higher </li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 25.0.3+ </li><li> Android Build Tools version 25.0.2 </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods (version 1.1.0 or higher) </li><li> iOS 9 or higher </li><li> MacOS 10.11.5 </li><li> Xcode 8.1 25.0.3+ </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> The Cloud Foundry CLI </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> The Cloud Foundry CLI </li><li> Maven </li></ul></dd>
  </dl>
3. Click **Review Activity** to see the authentication events that have occurred. You should see at least one event if you have logged in.
4. Customize your login experience. You can select an image, such as your logo and a header color. You can select one of the color options or insert a hex value. When you are happy with the preview, click **Save Changes**. You can see an example of the sample sign in experience in the following image.
5. In your browser, refresh your login page. The changes that you made in the previous step are already visible.
