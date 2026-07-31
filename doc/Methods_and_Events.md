# Authentication Integration

The Touch Platform integrates with your application's authentication system through a small set of **methods** and **events**. These APIs allow the platform to identify authenticated users, initiate authentication flows, and remain synchronized with your application's authentication state.

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
| `getAuthorizationHeaders()` | Returns the HTTP headers required to authenticate requests. |  `Promise<string \| null>` |

---

# Events

Emit the following event whenever the user's authentication state changes.

| Event | Description | Payload |
|-------|-------------|---------|
| `authStateChanged` | Emitted whenever the user's authentication state changes (login, logout, session refresh, or session expiration). | `AuthState` |

> **Note**
>
> The `authStateChanged` event replaces separate login and logout events. The Touch Platform derives the current authentication state from the event payload, providing a simpler and more reliable integration.

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

---

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
        methods: {
          showLogin() {
            window.yourInterface.showLogin();
          },

          getUser() {
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

          getAuthorizationHeaders() {
            return {
              Authorization: `Bearer ${window.yourInterface.getAccessToken()}`
            };
          }
        }
      });
    }
  })(window, document, "script", "ecTouchPlatform");
</script>
```

---

# Best Practices

- Always return the expected TypeScript types.
- Resolve `login()` and `signup()` with an `AuthResult`. Avoid throwing exceptions for expected authentication failures such as invalid credentials.
- Return `null` from `getUser()` when no authenticated user exists.
- Emit `authStateChanged` immediately after any authentication state transition, including:
  - User signs in
  - User signs out
  - Session is refreshed
  - Session expires
- Keep the `User` object consistent throughout your application.
- Only expose user information required by the Touch Platform.
- Ensure `getAuthorizationHeaders()` always returns fresh authorization headers after access tokens are renewed.

---
