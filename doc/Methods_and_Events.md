## Methods and Events ##

Methods and Events are required for the Touch Platform to communicate with a client’s SSO solution to ensure that a user of content created on the Touch Platform is recognised by the client’s SSO solution.
The table below lists the Methods the Touch Platform initiates as calls from widgets  to obtain values dependant on the client’s SSO provider logic.
Please refer to the tables below with the list of Methods and Events.

#### Methods ####

Name | Description | A value must be returned
------------ | ------------ | ------------
showLogin | A method which handles the login callback. Use this method when you need to display the login modal. Method will be called from the widget side, depends on its logic. | void
getUserID | Retrieve logged in user ID from session | String or Integer
getUserProfile | Retrieve logged in user info from session | User Object 
isUserLoggedIn | Determines whether the current visitor is a logged in user | Boolean


#### Events ####

Name | Description | Params
------------ | ------------- | -------------
onLoginSuccess | Event should be fired whenever a user logs in successfully | User Object
onCancel | Invoked when a auth is canceled | -
onLogout | Event should be fired whenever a user logs out | -


#### User Object Structure ####

```javascript
{
    profile: {
        ref_id: "",
        name: "",
        email: ""
    }
}
```                  
                                  
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
              // SSO provider logic goes here. For example:
              // return window.yourInterface.viewLoginSignup();
          },
          getUserID: function() {
              // SSO provider logic goes here. For example:
              // return window.yourInterface.getCurrentUserID();
          },
          getUserProfile: function() {
              // SSO provider logic goes here. For example:
              // return window.yourInterface.getUserProfile();
          },
          isUserLoggedIn: function() {
              // SSO provider logic goes here. For example:
              // return window.yourInterface.isLoggedIn();
          },
      },
      events: function() {
          // SSO provider logic goes here. For example:
          
          const eventEmitter = window.yourInterface.getEventEmitter();

          eventEmitter.on('onLoginSuccess', function() {
              // Fire onLoginSuccess event
              window.ecTouchPlatform.events.emit('onLoginSuccess', UserObject});
          });
          
          eventEmitter.on('onCancel', function() {
              // Fire onCancel event
              window.ecTouchPlatform.events.emit('onCancel');
          });

          eventEmitter.on('onLogout', function() {
              // Fire onLogout event
              window.ecTouchPlatform.events.emit('onLogout');
          });
      },
  });
  </script>
```

