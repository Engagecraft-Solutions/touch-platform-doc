# touch-platform-doc

### Touch Widget Implementation || using web-component

To be able to publish from the Touch platform to your website or app, requires a simple script of web-component to be added to your page.

By following the 2 steps below, you will be set up and ready to go:

**STEP 1 (To be done once)**: Add the below code, if you want to be able to use widgets on your platform. You can either add this per page or put it in a central place (depending on your CMS setup).  We recommend putting this in a central place by inserting the script in the <HEAD> tag. This script will create a new custom HTML element called: <ec-touch-global></ec-touch-global>

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

**STEP 2 (Each time you wish to publish a widget)**: Include this tag anywhere in your main pages, where you want to include the widget. Simply copy the widget embed code from the Touch platform and insert it in the <BODY> tag.
  
### Example of STEP 1 and STEP 2: ###

```javascript
<!doctype html>
<html class="no-js" lang="en">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>PlayGround</title>
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
