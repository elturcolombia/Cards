# Title: Use Laravel Socialite for OAuth Authentication

- **Date:** 2025-09-28
- **Status:** Accepted

## Context

The application needs to support social logins, starting with Google, to provide a seamless user registration and login experience. We considered two main alternatives:

1.  Build the OAuth2 flow manually.
2.  Use a pre-existing, well-maintained library.

Manually implementing OAuth2 is complex, time-consuming, and prone to security errors. It requires handling state, tokens, and specific API requirements for each provider.

## Decision

We will use the official `laravel/socialite` package to handle all OAuth operations. It is the standard, recommended library for this purpose within the Laravel ecosystem.

## Consequences

### Positive
-   **Drastically Reduced Development Time:** It provides a simple, fluent interface that abstracts away the complexity of the OAuth2 flow.
-   **Improved Security:** Relies on a package that is vetted and used by thousands of applications, reducing the risk of implementation errors.
-   **Easily Extensible:** Adding other providers in the future (e.g., Facebook, GitHub, Twitter) is trivial and follows the same pattern.
-   **Well-Documented and Maintained:** As an official Laravel package, it has excellent documentation and community support.

### Negative
-   **Adds an External Dependency:** The project now depends on an external package and its maintenance cycle.
