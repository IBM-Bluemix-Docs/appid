---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Using the OIDC discovery endpoint
{: #discovery}

OpenID Connect supports a discovery protocol that contains information that you can use to configure your apps and authenticate users such as tokens and public keys.
{: shortdesc}


## Calling the endpoint
{: #call-wellknown}

You can obtain the discovery document and the information that it contains by calling the `.well-known` endpoint.
{: shortdesc}


**Where can I find the endpoint?**

You can find the endpoint at the following URL:

  ```
  https://[region].appid.cloud.ibm.com/oauth/v3/{tenantId}/.well-known/openid-configuration
  ```
  {: codeblock}

</br>

**How do I make the call to the endpoint?**

To make a call to the endpoint you must have a valid `tenantID` and you must hardcode the discovery document URI in your application.

Check out the following sample cURL request:

  ```bash
  curl -X GET --header 'Accept: application/json'  'https://us-south.appid.cloud.ibm.com/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/.well-known/openid-configuration'
  ```
  {:codeblock}

</br>

**What can I expect the call to return?**

The response should look similar to the following example:

  ```bash
  {
    "issuer" : "us-south.appid.cloud.ibm.com",
    "authorization_endpoint": "https://us-south.appid.cloud.ibm.com/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/authorization",
    "token_endpoint": "https://us-south.appid.cloud.ibm.com/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/token",
    "jwks_uri": "https://us-south.appid.cloud.ibm.com/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/publickeys",
    "subject_types_supported": [
      "public"
    ],
    "id_token_signing_alg_values_supported": [
      "RS256"
    ],
    "userinfo_endpoint": "https://us-south.appid.cloud.ibm.com/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/userinfo",
    "scopes_supported": [
      "openid"
    ],
    "response_types_supported": [
      "code"
    ],
    "claims_supported": [
      "iss",
      "aud",
      "exp",
      "tenant",
      "iat",
      "sub",
      "nonce",
      "amr",
      "oauth_client"
    ],
    "grant_types_supported": [
      "authorization_code",
      "password",
      "refresh_token",
      "client_credentials",
      "urn:ietf:params:oauth:grant-type:jwt-bearer"
    ],
    "profiles_endpoint": "https://us-south.appid.cloud.ibm.com/",
    "service_documentation": "https://cloud.ibm.com/docs/services/appid/index.html"
  }
  ```
  {: screen}

  <table>
    <tr>
      <th> Component </th>
      <th> Description </th>
    </tr>
    <tr>
    <td><code>issuer</code></td>
    <td>The location of the OIDC provider.</td>
    </tr>
    <tr>
      <td><code>authorization_endpoint</code></td>
      <td>The URL of the {{site.data.keyword.appid_short_notm}} OAuth 2.0 authorization endpoint.</td>
    </tr>
    <tr>
      <td><code>token_endpoint</code></td>
      <td>The URL of the {{site.data.keyword.appid_short_notm}} OAuth 2.0 token endpoint.</td>
    </tr>
    <tr>
      <td><code>jwks_uri</code></td>
      <td>The URL of the {{site.data.keyword.appid_short_notm}} web key set document.</td>
    </tr>
    <tr>
      <td><code>subject_types_supported</code></td>
      <td>A JSON array that contains a list of the subject identifier types that {{site.data.keyword.appid_short_notm}} supports.</td>
    </tr>
    <tr>
      <td><code>id_token_signing_alg_values_supported</code></td>
      <td>A JSON array that contains a list of the JWS signing algorithms that the {{site.data.keyword.appid_short_notm}} server supports.</td>
    </tr>
    <tr>
      <td><code>userinfo_endpoint</code></td>
      <td>The URL of the {{site.data.keyword.appid_short_notm}} userinfo endpoint.</td>
    </tr>
    <tr>
      <td><code>scopes_supported</code></td>
      <td>A JSON array that contains a list of the OAuth 2.0 scope values that {{site.data.keyword.appid_short_notm}} supports.</td>
    </tr>
    <tr>
      <td><code>response_types_supported</code></td>
      <td>A JSON array that contains a list of the OAuth 2.0 response_type values that {{site.data.keyword.appid_short_notm}} supports.</td>
    </tr>
    <tr>
      <td><code>claims_supported</code></td>
      <td>A JSON array that contains a list of the claim names.</td>
    </tr>
    <tr>
      <td><code>grant_types_supported</code></td>
      <td>A JSON array that contains a list of the OAuth 2.0 grant type values that {{site.data.keyword.appid_short_notm}} supports.</td>
    </tr>
    <tr>
      <td><code>profiles_endpoint</code></td>
      <td>The URL of the {{site.data.keyword.appid_short_notm}} user profile endpoint.</td>
    </tr>
  </table>

</br>
</br>


