## Methods and Events

The Touch Platform uses **methods** and **events** to integrate with a client’s Single Sign-On (SSO) system.
These allow the platform to identify users and synchronize authentication state between the widget and your application.

> ⚠️ **Web Component Only**
> Methods and events are only available when using the Web Component integration.
> They are not supported in iFrame implementations.

---

## 🔧 Methods

The following methods must be implemented to enable authentication and user data retrieval:

| Name               | Description                                         | Return Value                         |
| ------------------ | --------------------------------------------------- | ------------------------------------ |
| `showLogin`        | Displays the login/signup interface                 | `void`                               |
| `isUserLoggedIn`   | Returns whether the current user is authenticated   | `boolean`                            |
| `getCurrentUserID` | Returns the unique identifier of the logged-in user | `string \| number`                   |
| `getUserProfile`   | Returns the current user’s profile data             | `UserObject`                         |
| `doLogin`          | Initiates login via your SSO system                 | `Promise<AuthSuccess \| AuthFailed>` |
| `doSignup`         | Initiates signup via your SSO system                | `Promise<AuthSuccess \| AuthFailed>` |

---

## 📡 Events

The following events must be emitted to notify the Touch Platform about authentication state changes:

| Name             | Description                            | Parameters   |
| ---------------- | -------------------------------------- | ------------ |
| `onLoginSuccess` | Fired when a user successfully logs in | `UserObject` |
| `onLogout`       | Fired when a user logs out             | `-`          |

---

## 🧩 Data Structures

### `UserObject`

```json id="f6v1z3"
{
  "id": "",
  "name": "",
  "email": ""
}
```

---

### `AuthSuccess`

```json id="r0k9lp"
{
  "success": true,
  "user": {
    "id": "",
    "name": "",
    "email": ""
  }
}
```

---

### `AuthFailed`

```json id="x2p8mw"
{
  "success": false,
  "errorMessage": "An error occurred."
}
```

---

## 💡 Integration Example

```html id="n7q4sd"
<script>
  !function(t, e, n, i, o, c) {
    if (!t[i]) {
      t[i] = function() {
        (t[i].init = []).push(arguments[0]);
      },
      o = e.createElement(n),
      c = e.getElementsByTagName(n)[0],
      o.defer = 1,
      o.async = 1,
      o.src = "https://widgets.touch.global/sdk/index.js",
      c.parentNode.insertBefore(o, c);

      t[i]({
        methods: {
          showLogin: function() {
            window.yourInterface.viewLoginSignup();
          },
          isUserLoggedIn: function() {
            return window.yourInterface.isLoggedIn();
          },
          getCurrentUserID: function() {
            return window.yourInterface.getCurrentUserID();
          },
          getUserProfile: function() {
            return window.yourInterface.getUserProfile();
          },
          doLogin: function(credentials) {
            return window.yourInterface.login(
              credentials.email,
              credentials.password
            );
          },
          doSignup: function(payload) {
            return window.yourInterface.signup(
              payload.email,
              payload.password
            );
          }
        },

        events: function() {
          const eventEmitter = window.yourInterface.getEventEmitter();

          eventEmitter.on("onLoginSuccess", function(user) {
            window.ecTouchPlatform.events.emit("onLoginSuccess", user);
          });

          eventEmitter.on("onLogout", function() {
            window.ecTouchPlatform.events.emit("onLogout");
          });
        }
      });
    }
  }(window, document, "script", "ecTouchPlatform");
</script>
```

---

## ✅ Notes & Best Practices

* Ensure all methods return the correct types as defined above
* Always resolve/reject Promises for `doLogin` and `doSignup`
* Emit events immediately after authentication state changes
* Keep your `UserObject` consistent across all methods and events
* Avoid exposing sensitive user data beyond what is required

---
