# Yamkins

Jenkins plugin that posts notifications to Yammer groups written in Java. Please note, this plugin is under development
and is not yet working.

The plugin draws ideas and code from the similar [jenkins-hipchat-plugin](https://github.com/jlewallen/jenkins-hipchat-plugin). Thanks!

*Beware:* The rate limit for messages is 10 requests in 30 seconds. Rate limits are not respected by this plugin. However, for small and medium sized Jenkins installations this should never become a problem.

## Requirements

* A Yammer user account
* A Yammer group

## Installation



## Configuration

- Acquire a long-lived access token as described further below.
- Enter it in the global Jenkins configuration
- Set up a post-build notification in your desired job and enter the group ID.

## License

The plugin is licensed using the [MIT License](http://opensource.org/licenses/MIT). See the LICENSE file in the root directory.

# Yammer

## Get API token (manual OAuth procedure)

1. Go to [Yammer Client Applications](https://www.yammer.com/client_applications) to register your app
2. Click on "Click here to register a new app"
3. Enter details, along these lines:
	* *Application name:* Build Server Notifications
	* *Organization:* Engineering
	* *Support e-mail:* your e-mail adress or an engineering mailing list
	* *Website:* anything, maybe an internal wiki site
4. Take note of the client ID and secret on the following application details page.
5. Get the client token according to the steps on https://developer.yammer.com/authentication/ or listed here:
6. Log into Yammer with a user account that you like your Jenkins build notifications get posted with
7. Fill in client\_id and any webpage here:
        https://www.yammer.com/dialog/oauth?client_id=[:client_id]&redirect_uri=[:redirect_uri]
8. Click "Allow"
9. You will be forwarded to an URL copy the code from it:
        https://www.yammer.com/<URL>/?code=njNBNwmiJlYZheu917Dtw
10. Use this code in this URL, the client ID and secret you already have from step 4.
        https://www.yammer.com/oauth2/access_token.json?client_id=[:client_id]&client_secret=[:client_secret]&code=[:code]
11. In the returned JSON, find access\_token.token property. This will be your single, long-lived API token to set-up in the Yamkins configuration.

## Create Yammer network for testing

1. Go to https://www.yammer.com/signup
2. Enter an e-mail address of an existing network you may join or a new one (depends on the hostname)
3. Verify e-mal address
4. Complete registration process

# Development

## Debugging the plugin with Intellij IDEA

As described at the [Jenkins website](https://wiki.jenkins-ci.org/display/JENKINS/Plugin+tutorial#Plugintutorial-DebuggingaPlugin), create a new maven run configuration with the
hpi:run goal and the following parameters in the Runner-VM Options:

> -Xdebug -Xrunjdwp:transport=dt_socket,server=y,address=8000,suspend=n

Jenkins will then be available at http://localhost:8080/

## Known Issues

- A NoSuchFileException is thrown under windows due to the known issue [JENKINS-17681](bug: https://issues.jenkins-ci.org/browse/JENKINS-17681).

## Ideas

- Mapping Jennkins to users to Yammer user IDs to somehow CC users that started builds.
- Validate the access token on the click of a button.
