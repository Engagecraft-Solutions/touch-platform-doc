# Authentication Integration

The Touch Platform integrates with your application's authentication system through a small set of methods and events.

These APIs allow the platform to:

- Identify authenticated users
- Trigger your application's login flow
- Synchronize authentication state
- Authenticate backend requests
- React to runtime configuration changes

> **Web Component Only**
>
> Authentication integration is supported **only** by the **Web Component** integration.
> It is **not available** when using the iFrame integration.

---

# Configuration

The following initialization options control how the Touch Platform integrates with your authentication system.

| Option | Type | Description |
|--------|------|-------------|
| `waitForSSO` | `boolean` | Delays widget and layout rendering until the initial authentication state has been resolved. The platform waits for either `getUser()` to resolve or the first `authStateChanged` event. If no authenticated user is available (`getUser()` returns `null` or `authStateChanged` is emitted with `authenticated: false`), the render lock is released and the widget starts in the anonymous state. |
| `authGuard` | `string` | Identifies the authentication provider used by your application. When specified, the Touch Platform sends the `x-api-client-auth-provider` header together with authenticated requests. This allows the backend to determine how the `Authorization` header should be validated. This option is only applicable when `getAuthorizationHeaders()` is implemented. |

---

# Methods

Implement the following methods when initializing the widget.

| Method | Returns | Description |
|---------|---------|-------------|
| `showLogin()` | `void` | Opens your application's login or sign-up UI. |
| `getUser()` | `User \| null` | Returns the currently authenticated user. |
| `login(credentials)` | `Promise<AuthResult>` | Authenticates a user. |
| `signup(payload)` | `Promise<AuthResult>` | Registers a new user. |
| `getAuthorizationHeaders()` | `Promise<Record<string, string> \| null>` | Returns fresh authorization headers for authenticated backend requests. |

---

# Events

The Touch Platform communicates with the host application through the following events.

| Event | Payload | Description |
|------|---------|-------------|
| `attributeChanged` | `AttributeChangedEvent` | Applies supported runtime configuration changes without reloading the widget. |
| `authStateChanged` | `AuthState` | Synchronizes authentication state with the Touch Platform. |
| `reloadWidget` | `void` | Requests a complete widget reinitialization. |

> **Important**
>
> Always emit `authStateChanged` immediately after any authentication state transition.

---

# Types

## User

```ts
export interface User {
  id: string;
  name: string;
  email: string;
}
```

## LoginCredentials

```ts
export interface LoginCredentials {
  email: string;
  password: string;
}
```

## SignupPayload

```ts
export interface SignupPayload {
  email: string;
  password: string;
}
```

## AuthSuccess

```ts
export interface AuthSuccess {
  success: true;
  user: User;
}
```

## AuthFailed

```ts
export interface AuthFailed {
  success: false;
  error: string;
}
```

## AuthResult

```ts
export type AuthResult = AuthSuccess | AuthFailed;
```

## AuthState

```ts
export interface AuthState {
  authenticated: boolean;
  user: User | null;
}
```

---

# Event Behavior

## authStateChanged

Emit this event whenever authentication changes, including:

- User signs in
- User signs out
- Session refresh
- Session expiration
- User profile updates

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

If:

- `authenticated === false`, or
- `user === null`

the Touch Platform automatically terminates its authenticated session and switches to anonymous mode.

---

## reloadWidget

Recreates the widget using the latest configuration.

When handling this event:

- Destroy the current widget instance.
- Clear any runtime state.
- Initialize a new widget using the latest configuration and authentication state.

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
      waitForSSO: true,
      authGuard: "gh-epl",

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

      onLoaded(touch) {
        const eventEmitter = window.yourInterface.getEventEmitter();

        eventEmitter.on("onLoginSuccess", function (data) {
          touch.events.emit("authStateChanged", {
            authenticated: true,
            user: {
              id: data.id,
              name: data.name,
              email: data.email
            }
          });
        });

        eventEmitter.on("onLogout", function () {
          touch.events.emit("authStateChanged", {
            authenticated: false,
            user: null
          });
        });
      }
    });
  }
})(window, document, "script", "ecTouchPlatform");
</script>
```

---

# Best Practices

- Always return the expected TypeScript types.
- Return `null` from `getUser()` when no user is authenticated.
- Resolve `login()` and `signup()` with an `AuthResult`. Do not throw for expected authentication failures.
- Always emit `authStateChanged` after authentication changes.
- Keep the `User` object consistent throughout your application.
- Return fresh authorization headers after token renewal.
- Use `waitForSSO` when authentication must be resolved before rendering.
- Use `authGuard` only together with `getAuthorizationHeaders()`.
- Prefer `attributeChanged` over `reloadWidget` whenever possible.
