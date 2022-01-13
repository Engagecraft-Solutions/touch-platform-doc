## Methods and Events ##

Methods and Events are required for the Touch Platform to communicate with a client’s SSO solution to ensure that a user of content created on the Touch Platform is recognised by the client’s SSO solution.
The table below lists the Methods the Touch Platform initiates as calls from widgets  to obtain values dependant on the client’s SSO provider logic.
Please refer to the tables below with the list of Methods and Events.

#### Methods ####

Name | Description | A value must be returned
------------ | ------------- | -------------
showLogin | A method which handles the login callback. Use this method when you need to display the login modal. Method will be called from the widget side, depends on its logic. | void
getUserID | Retrieve logged in user ID from session | String or Integer
getUserProfile | Retrieve logged in user info from session - ```{name: "", email: ""}``` | Object 
isUserLoggedIn | Determines whether the current visitor is a logged in user | Boolean
onEvent | [in progress] | 

The table below lists the Events [Events inform the widgets for them to know that user is logged in or logged out ().].

#### Events ####

Name | Description | Params
------------ | ------------- | -------------
onLoginSuccess | Should be fired whenever a user successfully logs in | -
onRegistrationSuccess | | -
onCancel | | -
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
          getUserProfile: function() {
              // your SSO provider logic goes here...
          },
          isUserLoggedIn: function() {
              // your SSO provider logic goes here...
          },
          onEvent: function(event) {
              // your logic goes here...
          },
      },
      events: function() {
          // your SSO provider logic goes here... 
          // for example:
          
          const yourEventEmitter = window.yourSSOProvider.getEventEmitter();

          eventEmitter.on('login', function() {
              // Fire onLogin event
              window.ecTouchPlatform.events.emit('onLoginSuccess');
          });
          
         eventEmitter.on('registration', function() {
              // Fire onLogin event
              window.ecTouchPlatform.events.emit('onRegistrationSuccess');
          });
          
          eventEmitter.on('cancel', function() {
              // Fire onCancelLogin event
              window.ecTouchPlatform.events.emit('onCancel');
          });

          eventEmitter.on('logout', function() {
              // Fire onLogout event
              window.ecTouchPlatform.events.emit('onLogout');
          });
      },
  });
  </script>
```

