**STEP 1**: Add the below code, if you want to be able to use widgets on your platform. You can either add this per page or put it in a central place (depending on your CMS setup).  We recommend putting this in a central place by inserting the script in the HEAD tag.

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
             showLogin() {
                window.ocUser.viewLoginSignup();
            },
            isUserLoggedIn() {
                return window.ocUser.isLoggedIn();
            },
            getCurrentUserID() {
                return window.ocUser.getCurrentUserID();
            },
            getUserProfile() {
                var profile = window.ocUser.getUserProfile();
                if (profile.isLoggedIn === true) {
                    return { user: { id: profile.id, email: profile.email } };
                }
                return null;
            },
            doLogin(credentials) {
                return window.ocUser.login(credentials.email, credentials.password).then((response) => {
                    if (response.success === true) {
                        return { success: true, user: { id: response["user-id"] } };
                    } else {
                        return { success: false, errorMessage: response.message };
                    }
                });
            },
            doSignup(payload) {
                return window.ocUser.signup(payload.email, payload.password).then((response) => {
                    if (response.success === true) {
                        return { success: true, user: { id: response["user-id"] } };
                    } else {
                        return { success: false, errorMessage: response.message };
                    }
                });
            }
        }
      });
    }
  }(window, document, "script", "ecTouchPlatform");
</script>
```

**STEP 2 (Each time you wish to publish a widget)**: Include this tag anywhere in your HTML pages, where you want to include the widget. Simply copy the widget embed code from the Touch platform and insert it in the BODY tag. The above script registers new HTML element called "ec-touch-global" and this new element can be used anywhere in your HTML page.

