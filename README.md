# Touch Platform Documentation

## Overview

This guide explains how to integrate **Touch widgets** into your website or application using either:

* Web Components (recommended)
* iFrame embedding
* Native in-app WebViews (Android / iOS)

Touch widgets allow you to easily publish interactive content with minimal setup.

---

## 🚀 Quick Start (Web Component – Recommended)

### Step 1: Load the Touch SDK

Add the following script to your HTML.
For best performance, include it globally in the `<head>` section.

```html
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
    }
  }(window, document, "script", "ecTouchPlatform");
</script>
```

---

### Step 2: Add the Widget

Insert the custom element anywhere in your `<body>` where the widget should appear:

```html
<ec-touch-global id="YOUR_WIDGET_HASH" language="en"></ec-touch-global>
```

---

### ✅ Full Example

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <meta name="mobile-web-app-capable" content="yes">
  <title>Touch Widget Example</title>

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
      }
    }(window, document, "script", "ecTouchPlatform");
  </script>
</head>
<body>
  <ec-touch-global id="7-BGRSFilRpfOo6D" language="en"></ec-touch-global>
</body>
</html>
```

---

## ⚙️ Widget Parameters

| Parameter  | Description              | Example            |
| ---------- | ------------------------ | ------------------ |
| `hash`     | Unique widget identifier | `7-BGRSFilRpfOo6D` |
| `language` | Widget language          | `en`               |
| `demo`     | Enable demo mode         | `true`             |
| `source`   | Custom source tracking (overrides  document.referrer)   | `homepage` |
| `tag`   | Custom campaign tracking   | `brandA` |

---

## 📡 Methods & Events

Touch widgets expose methods and events for advanced control and integrations.

👉 Documentation:
https://github.com/Engagecraft-Solutions/touch-platform-doc/blob/main/doc/Methods_and_Events.md

---

## 🔗 Live Demo

* Web Component: https://jsfiddle.net/vn1fk5jc/

---

## 🧩 Alternative: iFrame Integration

If Web Components are not suitable for your environment, you can embed widgets using an iFrame.

### Example

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Touch Widget iFrame</title>
</head>
<body>
  <iframe 
    src="https://widgets.touch.global/sdk/iframe.html?language=en&hash=7-BGRSFilRpfOo6D"
    width="100%" 
    height="540px" 
    frameborder="0">
  </iframe>
</body>
</html>
```

---

### 🔗 Live Demo (iFrame)

https://jsfiddle.net/yon0qbje/

---

## 📱 In-App Integration (experimential)

Touch widgets can also be embedded inside mobile apps using WebViews.

### Android

👉 https://github.com/Engagecraft-Solutions/touch-platform-sdk-android

### iOS

👉 https://github.com/Engagecraft-Solutions/touch-platform-widgets-ios

---

## 💡 Best Practices

* Load the SDK once globally (avoid duplicate script loads)
* Use Web Components for best performance and flexibility
* Use iFrame only when isolation is required or when your CMS does not support Web Components
* Ensure responsive container sizing for optimal UX
* Cache or lazy-load widgets if used heavily on a page

---

## ❓ Support

If you encounter issues or need help integrating Touch widgets, please contact your platform provider or refer to the official repositories above.

---

## 📄 License

© Engagecraft. All rights reserved.

---
