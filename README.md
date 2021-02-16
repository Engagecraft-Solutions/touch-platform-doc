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

**STEP 2 (Each time you wish to publish a widget)**: Include this tag anywhere in your main pages, where you want to include the widget. Simply copy the widget embed code from the Touch platform and insert it in the BODY tag.
  
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

Methods and events is useful for making a communication between your SSO provider and Touch platform.

#### Methods ####

Name | Description
------------ | -------------
showLogin | A method which handles the login callback. Use this method when you need to display the login modal. Method will be called from the widget side, depends on its logic.
isLoggedIn | Description
getUserID | Description

#### Events ####

Name | Description
------------ | -------------
onLogin | Description
onLogout | Description

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
              // your SSO logic goes here....
              return window.yourSSOProvider.showLoginScreen();
          },
          isLoggedIn: function() {
              // your SSO logic goes here...
              return window.yourSSOProvider.isLogged();
          },
          getUserID: function() {
              // your SSO logic goes here...
              return window.yourSSOProvider.getCurrentUser();
          },
      },
      events: function() {
          // your SSO logic goes here...
          const eventEmitter = window.yourSSOProvider.getEventEmitter();

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


## Touch Widget Implementation || using WebView

If you want to deliver a web application (or just a web page) as a part of a client application, you can do it using WebView. The WebView class is an extension of Android's / iOS View class that allows you to display web pages as a part of your activity layout. It does not include any features of a fully developed web browser, such as navigation controls or an address bar. All that WebView does, by default, is show a web page.

#### Implementation using Android System WebView
coming soon...

#### Implementation using iOS System WebView
coming soon...
