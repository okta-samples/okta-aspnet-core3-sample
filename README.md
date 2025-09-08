# ASP.NET Core & Okta-Hosted Sign-In Page Example

This example shows you how to use the [Okta ASP.NET Core SDK] to sign in a user. The user's browser is first redirected to the Okta-hosted sign-in page. After the user authenticates, they are redirected back to your application. ASP.NET Core automatically populates `HttpContext.User` with the information Okta sends back about the user.

## Prerequisites

Before running this sample, you will need an Okta Integrator Free Plan account. To get one, sign up for an [Integrator account](https://developer.okta.com/login). Once you have an account, sign in to your [Integrator account](https://developer.okta.com/login). Next, in the Admin Console:

1. Go to **Applications > Applications**
2. Click **Create App Integration**
3. Select **OIDC - OpenID Connect** as the sign-in method
4. Select **Web Application** as the application type, then click **Next**
5. Enter an app integration name
6. Configure the redirect URIs:
- Accept the default redirect URI values:
- **Sign-in redirect URIs:**
  - `https://localhost:5001/authorization-code/callback`
  - `http://localhost:8080/authorization-code/callback`
- **Sign-out redirect URIs:**
  - `https://localhost:5001`
  - `http://localhost:8080`
7. In the **Controlled access** section, select the appropriate access level
8. Click **Save**

Creating an OIDC Web App manually in the Admin Console configures your Okta Org with the application settings. You may also need to configure trusted origins for `https://localhost:5001` and `http://localhost:8080` in **Security > API > Trusted Origins**.

## Running This Example

### Get the code

```bash
git clone https://github.com/okta-samples/okta-aspnet-core3-sample.git
cd okta-aspnet-core3-sample
```

Update your config file at `okta-aspnetcore-mvc-example/appsettings.json` with the values from your application's configuration:

```text
"OktaDomain": "https://dev-133337.okta.com",
"ClientId": "0oab8eb55Kb9jdMIr5d6",
"ClientSecret": "NEVER-SHOW-SECRETS"
```

### Where are my new app's credentials?

After creating the app, you can find the configuration details on the app’s **General** tab:
- **Client ID:** Found in the **Client Credentials** section
- **Client Secret:** Click **Show** in the **Client Credentials** section to reveal
- **Okta Domain:** Found in the **Issuer URI** field for the authorization server that appears by selecting **Security > API** from the navigation pane.

### Run the web application

Run the example with your preferred tool and write down the port of your web application to configure Okta afterwards.

> **NOTE:** This sample is using ASP.NET Core 3.1 which enforces HTTPS. This is a recommended practice for web applications. Check out [Enforce HTTPS in ASP.NET Core] for more details.

> Because of recent changes in [Set-Cookie behavior (SameSite)](https://web.dev/samesite-cookies-explained) this code will only work properly if it's configured to use https. Check out [Work with SameSite cookies in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/security/samesite?view=aspnetcore-3.1) for more details.

#### Run the web application from Visual Studio

If you run this project in Visual Studio it will start the web application on port 44314 using HTTPS. You can change this configuration in the `launchSettings.json` in the Properties folder.

#### Run the web application from dotnet CLI

If you run this project via the dotnet CLI it will start the web application on port 5001 using HTTPS. You can change this configuration in the `launchSettings.json` in the Properties folder.

Navigate to the folder where the project file is located and type the following:

```dotnet run```

#### Trust the local dev certificate if necessary

If you’ve never run an ASP.NET Core 3.x application before, you may notice a strange error page come up warning you that the site is potentially unsafe.
This is because ASP.NET Core creates an HTTPS development certificate for you as part of the first-run experience, but it still needs to be trusted. You can ignore the warning by clicking on Advanced and telling the browser that it’s okay to visit this site even though there is no certificate for it. Or you can trust the certificate to get rid of this warning, check out [Configuring HTTPS in ASP.NET Core across different platforms] for more details.

Click the **Sign In** link in the Home page and it will redirect you to the Okta hosted sign-in page.

You can sign in with the same account that you created when signing up for your Developer Org, or you can use a known username and password from your Okta Directory.

**Note:** If you are currently using your Developer Console, you already have a Single Sign-On (SSO) session for your Org.  You will be automatically signed into your application as the same user that is using the Developer Console.  You may want to use an incognito tab to test the flow from a blank slate.

[Okta ASP.NET Core SDK]: https://github.com/okta/okta-aspnet
[OIDC Web Application Setup Instructions]: https://developer.okta.com/authentication-guide/implementing-authentication/auth-code#1-setting-up-your-application
[Enforce HTTPS in ASP.NET Core]: https://docs.microsoft.com/en-us/aspnet/core/security/enforcing-ssl?view=aspnetcore-2.2&tabs=visual-studio
[Configuring HTTPS in ASP.NET Core across different platforms]:https://devblogs.microsoft.com/aspnet/configuring-https-in-asp-net-core-across-different-platforms/
[Sign Users in to Your Web Application guide]: https://developer.okta.com/guides/sign-into-web-app/aspnet/before-you-begin/
[Sign Users Out guide]: https://developer.okta.com/guides/sign-users-out/aspnetcore/before-you-begin/
[Okta Developer Console]: https://login.okta.com
