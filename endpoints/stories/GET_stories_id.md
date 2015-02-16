# Stories Resources

    GET stories/:id

## Description
Returns detailed information of a single story.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: Bearer access_token

An example call with CURL:

     curl --header "Authorization: Bearer ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/stories/42

## Return format
A JSON object describing the Story object. A User object describing the author of the story is avaible inside the `user` key in **small format**.

Story object:

- **id** - ID of the story.
- **represent_txt** - Tells how the user uses Teen Quotes and why it is useful for him
- **frequence_txt** - Tells how often the user uses Teen Quotes and in which context
- **user_id** - ID of the author of the story.
- **created_at** - Date telling when the story was submitted.
- **updated_at** - Date telling when the story was edited.


User object:

- **id** - ID of the user.
- **login** - Login of the user.
- **profile_hidden** - Tells if the profile of the user should be hidden.
- **url_avatar** - Full URL of the user's avatar.
- **wants_notification_comment_quote** - Tells if the user wants to be notified when a comment is added on one of its quotes.
- **is_admin** - True if the user is an administrator.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **404 Not Found** — Story with the specified ID does not exist.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/stories/10

### Success
**Return**
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
For an error with HTTP code 404:
``` json
{
   "status":"story_not_found",
   "error":"The story #10 was not found."
}
```