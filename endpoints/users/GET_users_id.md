# Users Resources

    GET users/:id

## Description
Returns detailed information of a user.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/users/42

## Return format
A JSON object containing keys **country_object** and **newsletters**, where **country_object** is a Country object in **small format** and **newsletters** is a list of Newsletter object associated with the user in the following format:

- **user_id** — The ID of the user subscribed to the newsletter.
- **type** — The type of the newsletter. Possible values: daily|weekly
- **created_at** - Indicates when the object was created

The **country_object** as got the following format:

- **id** - ID of the country
- **name** - English name of the country

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **404 Not Found** — User with the specified ID does not exist.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/users/42

**Return**
``` json
{
   "id":"42",
   "login":"antoineaugusti",
   "email":"anonymous@gmail.com",
   "birthdate":"1980-08-01",
   "gender":"M",
   "country":"107",
   "city":"Lake Demetriusstad",
   "about_me":"Est excepturi laudantium repellendus totam recusandae sed quod. Rerum necessitatibus repellendus autem doloremque dolorum at. Est fuga adipisci mollitia fuga placeat maiores.",
   "last_visit":"2014-05-22 13:41:07",
   "created_at":"2014-05-19 12:46:56",
   "profile_hidden":true,
   "url_avatar":"http:\/\/teen-quotes.com\/uploads\/avatar\/42.jpg",
   "wants_notification_comment_quote":true,
   "is_admin":true,
   "country_object":{
      "id":"107",
      "name":"Jordan"
   },
   "newsletters":[
      {
         "user_id":"42",
         "type":"daily",
         "created_at":"2014-05-22 19:05:11"
      },
      {
         "user_id":"42",
         "type":"weekly",
         "created_at":"2014-05-22 19:05:11"
      }
   ],
   "total_comments":12,
   "favorite_count":14,
   "added_fav_count":23,
   "published_quotes_count":8
}
```

For an error with HTTP code 404:
``` json
{
   "status":404,
   "error":"User not found."
}
```