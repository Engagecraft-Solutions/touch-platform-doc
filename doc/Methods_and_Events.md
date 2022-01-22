## Methods and Events ##

Methods and Events are required for the Touch Platform to communicate with a client’s SSO solution to ensure that a user of content created on the Touch Platform is recognised by the client’s SSO solution. Please refer to the tables below.

#### Methods ####

Name | Description | Return Value
------------ | ------------ | ------------
showLogin | Display the login/signup modal | void
isUserLoggedIn | Determines whether the current visitor is a logged in user | Boolean
getCurrentUserID | Retrieve logged in user ID from session | String or Integer
getUserProfile | Retrieve logged in user info from session | <code>UserObject</code>
doLogin | Initiate a login call to the SSO API | <code>Promise<AuthSuccess &#124; AuthFailed></code>
doSignup | Initiate a signup call to the SSO API | <code>Promise<AuthSuccess &#124; AuthFailed></code>

#### Events #### 

Name | Description | Params
------------ | ------------- | -------------
onLoginSuccess | Event should be fired whenever a user logs in successfully | <code>UserObject</code>
onLogout | Event should be fired whenever a user logs out | -
    
#### <code>UserObject</code> ####

```javascript
{
    user: {
        id: "",
        name: "",
        email: ""
    }
}
```   

#### <code>AuthSuccess</code> ####

```javascript
{
    success: true,
    // UserObject
    user: {
        id: "",
        name: "",
        email: ""
    }
}
```  
 
#### <code>AuthFailed</code> ####

```javascript
{
    success: false,
    errorMessage: "An error occurred."
}
```     
    
#### Example ###

```javascript
<script>
  !function(t, e, n, i, o, c) {
    if (!t[i]) {
      t[i] = function() {
        (t[i].init = []).push(arguments[0]);
      }, o = e.createElement(n), c = e.getElementsByTagName(n)[0], o.defer = 1, o.async = 1, o.src = "https://widgets.touch.global/sdk/index.js", c.parentNode.insertBefore(o, c);
      t[i]({
        clientID: "bRUVL8o0KiMIDRBKojxECtTWp",
        methods: {
          showLogin: function() {
            window.yourInterface.viewLoginSignup();
          },
          getCurrentUserID: function() {
            return window.yourInterface.getCurrentUserID();
          },
          getUserProfile: function() {
            return window.yourInterface.getUserProfile();
          },
          isUserLoggedIn: function() {
            return window.yourInterface.isLoggedIn();
          },
          doLogin: function(credentials) {
            return window.yourInterface.login(credentials.email, credentials.password);
          },
          doSignup: function(payload) {
            return window.yourInterface.signup(payload.email, payload.password);
          },
        },
        events: function() {

          const eventEmitter = window.yourInterface.getEventEmitter();

          eventEmitter.on("onLoginSuccess", function() {
            // Fire onLoginSuccess event
            window.ecTouchPlatform.events.emit("onLoginSuccess", UserObject);
          });

          eventEmitter.on("onLogout", function() {
            // Fire onLogout event
            window.ecTouchPlatform.events.emit("onLogout");
          });
        }
      });
    }
  }(window, document, "script", "ecTouchPlatform");
</script>
```
