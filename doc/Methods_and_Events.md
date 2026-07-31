# Authentication Integration

The Touch Platform integrates with your application's authentication system through a small set of **methods** and **events**. These APIs allow the platform to identify authenticated users, initiate authentication flows, synchronize authentication state, and react to runtime configuration changes.

> ⚠️ **Web Component Only**
>
> Authentication methods and events are available **only** when using the **Web Component** integration. They are **not supported** when using the iFrame integration.

---

# Methods

Implement the following methods when initializing the Touch Platform.

| Method | Description | Returns |
|---------|-------------|---------|
| `showLogin()` | Opens your application's login or sign-up interface. | `void` |
| `getUser()` | Returns the currently authenticated user, or `null` if no user is signed in. | `User \| null` |
| `login(credentials)` | Authenticates a user using your application's authentication provider. | `Promise<AuthResult>` |
| `signup(payload)` | Registers a new user using your application's authentication provider. | `Promise<AuthResult>` |
| `getAuthorizationHeaders()` | Returns the HTTP authorization headers required to authenticate requests made by the Touch Platform. Always return fresh headers after access tokens are renewed. | `Promise<Record<string, string> \| null>` |

---

# Events

The Touch Platform communicates with the host application through the following events. These events keep authentication, widget lifecycle, and runtime configuration synchronized.

| Event | Description | Payload |
|-------|-------------|---------|
| `attributeChanged` | Emitted whenever one or more widget attributes are updated at runtime. Supported attributes (such as language, theme, currency, or other configuration values) are applied immediately without requiring a full widget reload. | `AttributeChangedEvent` |
| `authStateChanged` | Emitted whenever the user's authentication state changes, including login, logout, session refresh, session expiration, or profile updates. The Touch Platform synchronizes its SSO session using the provided authentication state and user information. | `AuthState` |
| `reloadWidget` | Requests a complete widget restart. The current instance is destroyed and a new instance is initialized using the latest configuration and authentication state. | `void` |

> **Note**
>
> `authStateChanged` is the primary event responsible for synchronizing authentication between the Touch Platform and the host application. Always emit this event immediately after any authentication state transition.

---

# TypeScript Types

## `User`

```ts
export interface User {
  id: string;
  name: string;
  email: string;
}
```

---

## `LoginCredentials`

```ts
export interface LoginCredentials {
  email: string;
  password: string;
}
```

---

## `SignupPayload`

```ts
export interface SignupPayload {
  email: string;
  password: string;
}
```

---

## `AuthSuccess`

```ts
export interface AuthSuccess {
  success: true;
  user: User;
}
```

---

## `AuthFailed`

```ts
export interface AuthFailed {
  success: false;
  error: string;
}
```

---

## `AuthResult`

```ts
export type AuthResult = AuthSuccess | AuthFailed;
```

---

## `AuthState`

```ts
export interface AuthState {
  authenticated: boolean;
  user: User | null;
}
```

# Event Behavior

## `authStateChanged`

Emit this event whenever the authentication state changes.

Examples include:

- User signs in
- User signs out
- Session is refreshed
- Session expires
- User profile information changes

Example:

```ts
{
  authenticated: true,
  user: {
    id: "123",
    name: "John Doe",
    email: "john@example.com"
  }
}
```

If either of the following conditions is true:

- `authenticated === false`
- `user === null`

the Touch Platform automatically terminates the authenticated SSO session and transitions to the anonymous state. The Touch Platform also clears its own temporary authenticated session.

---

## `reloadWidget`

Requests a complete widget restart.

When handled:

- the current widget instance should be destroyed;
- all runtime state should be discarded;
- a new widget instance should be initialized using the latest embed configuration and authentication state.

This event is typically used after configuration changes that cannot be applied dynamically.

# Integration Example

```html
<script>
  !(function (t, e, n, i, o, c) {
    if (!t[i]) {
      t[i] = function () {
        (t[i].init = []).push(arguments[0]);
      };

      o = e.createElement(n);
      c = e.getElementsByTagName(n)[0];
      o.async = true;
      o.src = "https://widgets.touch.global/sdk/index.js";
      c.parentNode.insertBefore(o, c);

      t[i]({
        waitForSSO: true,
        authGuard: 'gh-epl',
        onLoaded: (touch) => {}
        methods: {
          showLogin() {
            window.yourInterface.showLogin();
          },

          async getUser() {
            return window.yourInterface.getCurrentUser();
          },

          login(credentials) {
            return window.yourInterface.login(
              credentials.email,
              credentials.password
            );
          },

          signup(payload) {
            return window.yourInterface.signup(
              payload.email,
              payload.password
            );
          },

          async getAuthorizationHeaders() {
            return {
              Authorization: `Bearer ${window.yourInterface.getAccessToken()}`
            };
          }
        },
      });
    }
  })(window, document, "script", "ecTouchPlatform");
</script>
```

---

# Best Practices

- Always return the expected TypeScript types.
- Resolve `login()` and `signup()` with an `AuthResult`. Do not throw exceptions for expected authentication failures such as invalid credentials.
- Return `null` from `getUser()` whenever no authenticated user exists.
- Emit `authStateChanged` immediately after every authentication state transition, including login, logout, session refresh, session expiration, or user profile updates.
- Keep the `User` object consistent throughout your application. Only expose user information required by the Touch Platform
- Ensure `getAuthorizationHeaders()` always returns fresh authorization headers after access tokens are renewed.
- Prefer `attributeChanged` for runtime configuration updates instead of reloading the widget whenever supported.
- Use `reloadWidget` only when configuration changes require a complete reinitialization.
