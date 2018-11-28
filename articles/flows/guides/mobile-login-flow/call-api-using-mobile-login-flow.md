---
description: Learn how to call your API using the mobile login flow.
toc: true
topics:
  - api-authentication
  - oidc
  - authorization-code
  - pkce
contentType: tutorial
useCase:
  - secure-api
  - call-api
---
# Call Your API Using the Mobile Login Flow

<%= include('../../../_includes/_pipeline2') %>

::: note
This tutorial will help you call your API from a native/mobile app using the mobile login flow. If you want to learn how the flow works and why you should use it, see [Mobile Login Flow](/flows/concepts/mobile-login-flow).
:::

Auth0 makes it easy for your app to implement the mobile login flow using:

* [Auth0 Mobile SDKs](/libraries): The easiest way to implement the mobile login flow, which will do most of the heavy-lifting for you. Our [Mobile Quickstarts](/quickstart/native) will walk you through the process.
* Authentication API: If you prefer to roll your own, keep reading to learn how to call our API directly.

## Prerequisites

This tutorial can be used to call your API from a native/mobile app. If you want to learn to add login to your native/mobile app, see [Add Login to Your Native/Mobile App](/flows/guides/mobile-login-flow/add-login-using-mobile-login-flow).

**Before beginning this tutorial:**

* [Register the Application with Auth0](/applications/native). 
  * Select an **Application Type** of **Native**.
  * Add an **Allowed Callback URL** of **https://${account.namespace}/callback**.
  * Make sure the Application's **[Grant Types](/applications/application-grant-types#how-to-edit-the-application-s-grant_types-property)** include **Authorization Code**.

* [Register your API with Auth0](/architecture-scenarios/mobile-api/part-2#create-the-api)
  * Add an **Allowed Callback URL** of **com.myapi://myapi.com/callback**.
  * If you want your API to receive [Refresh Tokens](/tokens/refresh-token) to allow it to obtain new tokens when the previous ones expire, enable **Allow Offline Access**.

## Steps

1. [Create a code verifier](#create-a-code-verifier): 
Generate a `code_verifier` that will be sent to Auth0 to request tokens.
2. [Create a code challenge](#create-a-code-challenge): 
Generate a `code_challenge` from the `code_verifier` that will be sent to Auth0 to request an `authorization_code`.
3. [Authorize the user](#authorize-the-user): 
Request the user's authorization and redirect back to your app with an `authorization_code`.
4. [Request Tokens](#request-tokens): 
Exchange your `authorization_code` and `code_verifier` for tokens.
5. [Call Your API](#call-your-api):
Use the retrieved Access Token to call your API.
6. [Refresh Tokens](#refresh-tokens):
Use a refresh token to request new tokens.

Optional: [Explore Sample Use Cases](#sample-use-cases)



## Keep Reading

::: next-steps
- [Why you should always use Access Tokens to secure APIs](/api-auth/why-use-access-tokens-to-secure-apis)
- [The OAuth 2.0 protocol](/protocols/oauth2)
- [The OpenID Connect protocol](/protocols/oidc)
- [Tokens used by Auth0](/tokens)
:::