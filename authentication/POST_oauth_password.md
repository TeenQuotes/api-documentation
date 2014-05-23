# OAuth - Password grant

    POST https://api.teen-quotes.com/oauth

## Description
Allows an application to get an **access_token** that identifies a user. The **access_token** is required for all API calls.


## Parameters
The following parameters are required:

- **grant_type** — The grant method used for OAuth 2. It should be `password`
- **client_id** - The ID of the application requesting the **access_token**.
- **client_secret** - The secret passphrase of the application
- **username** - The login of the user. The **access_token** will authenticate this user after.
- **password** - The password of the user. It shouldn't be hashed.

Example POST request:
``` json
{
   "grant_type":"password",
   "client_id":"42",
   "client_secret":"IZgwaBTZ2EdtT3hT7UzG2rLQ8S0Vmu9GDxeHwcPz",
   "username":"antoineaugusti",
   "password":"iamawesome"
}
```

## Return format
A JSON object containing the following keys.

- **access_token** — The access token associated with the user
- **token_type** — The type of the token. It will be `bearer`
- **expires** - Tells when the access_token will expire as a UNIX timestamp.
- **expires_in** - The number of seconds that describes the validity of the access_token.
- **refresh_token** - The refresh token can be used to get a new access token when the current one expires.

Return example:
``` json
{
   "access_token":"IZgwaBTZ2EdtT3hT7UzG2rLQ8S0Vmu9GDxeHwcPz",
   "token_type":"bearer",
   "expires":1401437772,
   "expires_in":604800,
   "refresh_token":"x5Oewf7PUw38J07lwEnJXSyXolwZ1KMdxxH2bxFJ"
}
```


## Errors

### HTTP codes and `error` keys
If an error occurs, you will get a JSON object with the keys **error** and **error_description**.

- **400 Invalid OAuth Request** — When the **error** key has got one of the following values: `invalid_request`, `unauthorized_client`, `unsupported_response_type`, `invalid_scope`, `temporarily_unavailable`, `invalid_grant`, `invalid_credentials`, `invalid_refresh`.
- **401 Unauthorized** - When the **error** key has got one of the following values: `access_denied`, `invalid_client`.
- **501 Not Implemented** When the **error** key is `unsupported_grant_type`.

### error_description
The **error_description** messages are the following:

- `invalid_request` - The request is missing a required parameter, includes an invalid parameter value, includes a parameter more than once, or is otherwise malformed. Check the "%s" parameter.
- `unauthorized_client` - The client is not authorized to request an access token using this method.
- `access_denied` - The resource owner or authorization server denied the request.
- `unsupported_response_type` - The authorization server does not support obtaining an access token using this method.
- `invalid_scope` - The requested scope is invalid, unknown, or malformed. Check the "%s" scope.
- `server_error` - The authorization server encountered an unexpected condition which prevented it from fulfilling the request.
- `temporarily_unavailable` - The authorization server is currently unable to handle the request due to a temporary overloading or maintenance of the server.
- `unsupported_grant_type` - The authorization grant type "%s" is not supported by the authorization server
- `invalid_client` - Client authentication failed
- `invalid_grant` - The provided authorization grant is invalid, expired, revoked, does not match the redirection URI used in the authorization request, or was issued to another client. Check the "%s" parameter.
- `invalid_credentials` - The user credentials were incorrect.
- `invalid_refresh` - The refresh token is invalid.

Return example:
``` json
{
   "error":"invalid_request",
   "error_description":"The user credentials were incorrect."
}
```