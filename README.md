# touch-platform-doc

## Touch Widget Implementation || using web-component

[What are web components?](https://www.webcomponents.org/introduction) 

To be able to publish from the Touch platform to your website or app, requires a simple script of web-component to be added to your page.

By following the 2 steps below, you will be set up and ready to go:

**STEP 1**: Add the below code, if you want to be able to use widgets on your platform. You can either add this per page or put it in a central place (depending on your CMS setup).  We recommend putting this in a central place by inserting the script in the HEAD tag.

```javascript
<script>
  !function(t, e, n, i, o, c) {
    if (!t[i]) {
      t[i] = function() {
        (t[i].init = []).push(arguments[0]);
      }, o = e.createElement(n), c = e.getElementsByTagName(n)[0], o.defer = 1, o.async = 1, o.src = "https://widgets.touch.global/sdk/index.js", c.parentNode.insertBefore(o, c);
    }
  }(window, document, "script", "ecTouchPlatform");
</script>
```

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
      
  <script>
    !function(t, e, n, i, o, c) {
      if (!t[i]) {
        t[i] = function() {
          (t[i].init = []).push(arguments[0]);
        }, o = e.createElement(n), c = e.getElementsByTagName(n)[0], o.defer = 1, o.async = 1, o.src = "https://widgets.touch.global/sdk/index.js", c.parentNode.insertBefore(o, c);
      }
    }(window, document, "script", "ecTouchPlatform");
  </script>

</head>
<body>
  <ec-touch-global id="7-BGRSFilRpfOo6D" language="en"></ec-touch-global>
</body>
</html>
```

### Methods and Events
[Documentation](https://github.com/Engagecraft-Solutions/touch-platform-doc/blob/main/doc/Methods_and_Events.md) 

#### LIVE Example (updated 08 Jan 2024): ###
https://jsfiddle.net/vn1fk5jc/



## Touch Widget Implementation || using an Iframe

**STEP 1 (Each time you wish to publish a widget)**: Include iframe tag anywhere in your HTML pages, where you want to include the widget. Simply copy the widget embed code from the Touch platform and insert it in the BODY tag.

```javascript
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <meta name="mobile-web-app-capable" content="yes">
  <title>Touch Widget Implementation</title>
</head>
<body>
 <iframe src="https://widgets.touch.global/sdk/iframe.html?language=en&hash=7-BGRSFilRpfOo6D" width="100%" height="540px" frameBorder="0"></iframe>
</body>
</html>
```

#### LIVE Example (updated 08 Jan 2024): ###
https://jsfiddle.net/yon0qbje/

## Parameters (using web-component / using an Iframe)

Name | Description | Example
------------ | ------------ | ------------
hash | - | -
language | - | -
demo | - | -
source | - | -


## Touch Widget Implementation || In-App

Touch content is [published/delivered] using WebViews. The WebView class is an extension of the Android and iOS View Class that allows web pages to be displayed in-App.

### Implementation using In-App Android Integration
[Documentation](https://github.com/Engagecraft-Solutions/touch-platform-sdk-android) 

### Implementation using In-App iOS Integration
[Documentation](https://github.com/Engagecraft-Solutions/touch-platform-widgets-ios) 

