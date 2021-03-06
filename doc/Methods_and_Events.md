## Methods and Events ##

The Touch Platform uses an ‘indentificator’ to identify a client’s user. The identificator is a unique [attribute that identifies the user ] that is provided by the client.
‘Methods’ and ‘Events’ are required for the Touch Platform to communicate with a client’s SSO solution to ensure that a user of content created on the Touch Platform is recognised by the client’s SSO solution.
The table below lists the Methods the Touch Platform initiates as calls from widgets  to obtain values dependant on the client’s SSO provider logic.
Please refer to the tables below see below tables with the list of Methods and Events.

#### Methods ####

Name | Description | A value must be returned
------------ | ------------- | -------------
showLogin | A method which handles the login callback. Use this method when you need to display the login modal. Method will be called from the widget side, depends on its logic. | void
getUserID | Retrieve logged in user ID from session | String or Integer

The table below lists the Events [Events inform the widgets for them to know that user is logged in or logged out ().].

#### Events ####

Name | Description | Params
------------ | ------------- | -------------
onLogin | Should be fired whenever a user successfully logs in | userID
onLogout | Should be fired whenever a user logs out from SSO | -

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
          getUserID: function() {
              // your SSO provider logic goes here...
          },
      },
      events: function() {
          // your SSO provider logic goes here... 
          // for example:
          
          const yourEventEmitter = window.yourSSOProvider.getEventEmitter();

          eventEmitter.on('login', function(user) {
              // Fire onLogin event
              window.ecTouchPlatform.events.emit('onLogin', { userID: user.id });
          });

          eventEmitter.on('logout', function() {
              // Fire onLogout event
              window.ecTouchPlatform.events.emit('onLogout');
          });
      },
  });
  </script>
```


## Data capture and return to the client

Users’ engagement data collected on the Touch Platform is sent back to the client when the client requests this data via a rest API (using a client’s unique credentials).

## Touch Widget Implementation || In-App

Touch content is [published/delivered] using WebViews. The WebView class is an extension of the Android and iOS View Class that allows web pages to be displayed in-App.

#### Implementation using In-App Android Integration
The regular Javascrip embed code of a unit, once added to the article or webpage in your CMS will also work in In-App Android. The same is true for a header tag and playlist integration.

#### Implementation using In-App iOS Integration
The regular Javascrip embed code of a unit, once added to the article or webpage in your CMS will also work in In-App iOS. The same is true for a header tag and playlist integration.
