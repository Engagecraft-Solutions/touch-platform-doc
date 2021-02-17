# touch-platform-doc

## Touch Widget Implementation || using web-component

[What are web components?](https://www.webcomponents.org/introduction) 

To be able to publish from the Touch platform to your website or app, requires a simple script of web-component to be added to your page.

By following the 2 steps below, you will be set up and ready to go:

**STEP 1 (To be done once)**: Add the below code, if you want to be able to use widgets on your platform. You can either add this per page or put it in a central place (depending on your CMS setup).  We recommend putting this in a central place by inserting the script in the HEAD tag.

```javascript
<script>
  !function(t, e, n, i, o, c) {
    t[i] = t[i] || function() {
      (t[i].init = t[i].init || []).push(arguments[0]);
    }, o = e.createElement(n), c = e.getElementsByTagName(n)[0], o.defer = 1, o.async = 1, o.src = 'https://widgets.touch.global/sdk/index.js', c.parentNode.insertBefore(o, c);
  }(window, document, 'script', 'ecTouchPlatform');
  window.ecTouchPlatform({
    clientID: 'bRUVL8o0KiMIDRBKojxECtTWp',
  });
</script>
```
Initial settings:

Attribute | Default | Required | Description
------------ | ------------- | ------------- | -------------
clientID | bRUVL8o0KiMIDRBKojxECtTWp | true | demo client ID

**STEP 2 (Each time you wish to publish a widget)**: Include this tag anywhere in your HTML pages, where you want to include the widget. Simply copy the widget embed code from the Touch platform and insert it in the BODY tag. The above script registers new HTML element called "ec-touch-global" and this new element can be used anywhere in your HTML page.
  
### Example of STEP 1 and STEP 2: ###

```javascript
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <meta name="mobile-web-app-capable" content="yes">
  <title>Touch Widget Implementation</title>
    
  <link rel="preconnect" href="https://widgets.touch.global">
  
  <script>
    !function(t, e, n, i, o, c) {
      t[i] = t[i] || function() {
        (t[i].init = t[i].init || []).push(arguments[0]);
      }, o = e.createElement(n), c = e.getElementsByTagName(n)[0], o.defer = 1, o.async = 1, o.src = 'https://widgets.touch.global/sdk/index.js', c.parentNode.insertBefore(o, c);
    }(window, document, 'script', 'ecTouchPlatform');
    window.ecTouchPlatform({
      clientID: 'bRUVL8o0KiMIDRBKojxECtTWp',
    });
  </script>
  
</head>
<body>
  <ec-touch-global hash="3-QwbtYJWpUUxREoE"></ec-touch-global>
</body>
</html>
```
#### LIVE Example (updated 28 Jan 2021): ###
https://jsfiddle.net/EC_Touch_Platform/aktuczh5/

## Methods and Events ##

Touch does not save the user on Touch side, meaning that it saves only indentificator of the client user. Therefore, Methods and Events are needed to create a communication between your SSO provider and Touch platform. We provide list of Methods which we will initiate as a call from widgets side in order to get their values dependant on the SSO provider logic. Please see below tables with the list of Methods and Events.

#### Methods ####

Name | Description | A value must be returned
------------ | ------------- | -------------
showLogin | A method which handles the login callback. Use this method when you need to display the login modal. Method will be called from the widget side, depends on its logic. | void
isLoggedIn | Determines whether the current user is authenticated. | Boolean - true if the user has been authenticated; otherwise, false.
getUserID | Retrieve logged in user ID from session | String or Integer

#### Events ####

Name | Description
------------ | -------------
onLogin | Should be fired whenever a user successfully logs in
onLogout | Should be fired whenever a user logs out from SSO

### Example ###

```javascript
<script>
  !function(t, e, n, i, o, c) {
    t[i] = t[i] || function() {
      (t[i].init = t[i].init || []).push(arguments[0]);
    }, o = e.createElement(n), c = e.getElementsByTagName(n)[0], o.defer = 1, o.async = 1, o.src = 'https://widgets.touch.global/sdk/index.js', c.parentNode.insertBefore(o, c);
  }(window, document, 'script', 'ecTouchPlatform');
  window.ecTouchPlatform({
      clientID: 'bRUVL8o0KiMIDRBKojxECtTWp',
      methods: {
          showLogin: function() {
              // your SSO provider logic goes here....
          },
          isLoggedIn: function() {
              // your SSO provider logic goes here...
          },
          getUserID: function() {
              // your SSO provider logic goes here...
          },
      },
      events: function() {
          // your SSO provider logic goes here... 
          // for example:
          
          const yourEventEmitter = window.yourSSOProvider.getEventEmitter();

          eventEmitter.on('login', function() {
              // Fire onLogin event
              window.ecTouchPlatform.events.emit('onLogin');
          });

          eventEmitter.on('logout', function() {
              // Fire onLogout event
              window.ecTouchPlatform.events.emit('onLogout');
          });
      },
  });
  </script>
```
Even though, Touch is not providing separate solution on the SSO integration but rather adapts to the client’s solution, the engagement data we collect gets back to the client in the automated way using rest API. That is, client would just nee to call (using client’s unique credentials) our rest API in order to get the data we collect.

## Touch Widget Implementation || In-App

#### Implementation using In-App Android Integration
The regular Javascrip embed code of a unit, once added to the article or webpage in your CMS will also work in In-App Android. The same is true for a header tag and playlist integration.

#### Implementation using In-App iOS Integration
The regular Javascrip embed code of a unit, once added to the article or webpage in your CMS will also work in In-App iOS. The same is true for a header tag and playlist integration.
