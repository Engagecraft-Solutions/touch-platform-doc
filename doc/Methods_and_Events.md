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

```

