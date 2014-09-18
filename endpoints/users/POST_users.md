# Users Resources

    POST users

## Description
Create a new user.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

Since we can't have an **access_token** for the user that we will create, the application should provide its own **access_token**. To get one, use the [<code>client_credentials</code> method](https://github.com/TeenQuotes/api-documentation/blob/master/authentication/POST_oauth_client_credentials.md).

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/users

## Parameters
All parameters are required.

- **login** - The username of the user. Must be between 3 and 20 characters, can only contain alpha-numeric characters as well as dashes and underscores. Must not already exist in database.
- **password** - The password of the user. Must be at least 6 characters.
- **email** - The email address of the user. Must be a valid email address. Must not already exist in database.

Example request:

    curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" --data "login=newuser&password=azerty&email=testuser@teen-quotes.com" https://api.teen-quotes.com/v1/users

## Return format
A JSON object containing the User object that has just been created.

User object:

- **id** - ID of the user.
- **login** - Login of the user.
- **email** - Email address of the user.
- **last_visit** - Date of creation of the user.
- **created_at** - Date of creation of the user.

Some other computed attributes are added but they are not relevant.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad Request** — When the `status` key has got one of the following values: `wrong_login`, `wrong_password`, `wrong_email`.

### `error` messages
- If `status` is `wrong_login`: `The login must be at least 3 characters.`, `The login has already been taken.`, `The login may only contain letters, numbers, and dashes.`, `The login may not be greater than 20 characters.`
- If `status` is `wrong_password`: `The password must be at least 6 characters.`
- If `status` is `wrong_email`: `The email must be a valid email address.`, `The email has already been taken.`

## Example
**Request**

    POST https://api.teen-quotes.com/v1/users

### Success
With an HTTP code 201.
``` json
{
   "login":"newuser",
   "email":"testuser@teen-quotes.com",
   "last_visit":"2014-05-25 06:50:02",
   "created_at":"2014-05-25 06:50:02",
   "id":101,
   "profile_hidden":false,
   "url_avatar":"http:\/\/localhost:8000\/uploads\/avatar\/",
   "wants_notification_comment_quote":false,
   "is_admin":false
}
```

### Error
For an error with HTTP code 400:
``` json
{
   "status":"wrong_email",
   "error":"The email must be a valid email address."
}
```