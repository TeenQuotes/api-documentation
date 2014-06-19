# Stories Resources

    POST stories

## Description
Submit a new story.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/stories

## Parameters
All parameters are required.

- **represent_txt** - Tells how the user uses Teen Quotes and why it is useful for him. The content should be between 100 and 1,000 characters.
- **frequence_txt** - Tells how often the user uses Teen Quotes and in which context. The content should be between 100 and 1,000 characters.

Example request:

    curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" --data "represent_txt=Hello this is an amazing story it should be displayed&frequence_txt=Hello this is an amazing story it should be displayed" https://api.teen-quotes.com/v1/stories

## Return format
A JSON object containing the Story object that has just been created.

Story object:

- **id** - ID of the story.
- **represent_txt** - Tells how the user uses Teen Quotes and why it is useful for him
- **frequence_txt** - Tells how often the user uses Teen Quotes and in which context
- **user_id** - ID of the author of the story.
- **created_at** - Date telling when the story was submitted.
- **updated_at** - Date telling when the story was edited.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad Request** — When the `status` key has got one of the following values: `wrong_represent_txt`, `wrong_frequence_txt`.

### `error` messages
- If `status` is `wrong_represent_txt`: `The represent txt must be at least 100 characters.`, `The represent txt field is required.`, `The represent txt may not be greater than 1000 characters.`.
- If `status` is `wrong_frequence_txt`: `The frequence txt must be at least 100 characters.`, `The frequence txt field is required.`, `The frequence txt may not be greater than 1000 characters.`.

## Example
**Request**

    POST https://api.teen-quotes.com/v1/stories

### Success
``` json
{
   "id":10,
   "represent_txt":"Pariatur animi nihil soluta est minima et et. Neque magnam et id possimus numquam. Optio et sit voluptatum ipsum provident illo at. Veniam ipsa pariatur rerum et odio est temporibus. Deleniti alias dicta enim et molestiae quia. Sed voluptate est ipsam vel.",
   "frequence_txt":"Inventore at ut est aspernatur tenetur. Corrupti quidem suscipit necessitatibus et expedita neque vero. Ea officiis qui nulla harum incidunt molestias nulla. Maiores magni architecto dolorem. Velit voluptas qui recusandae ut et eum similique. Ut quia quibusdam non sint. Veniam quia aliquam laborum maiores non doloribus.",
   "user_id":4,
   "created_at":"2014-05-31 20:56:51",
   "updated_at":"2014-06-19 06:10:52",
   "user":{
      "id":4,
      "login":"cgjhr56",
      "profile_hidden":false,
      "url_avatar":"http:\/\/placekitten.com\/400\/400",
      "wants_notification_comment_quote":false,
      "is_admin":false
   }
}
```

### Error
For an error with HTTP code 400:
``` json
{
   "status":"wrong_frequence_txt",
   "error":"The frequence txt must be at least 100 characters."
}
```