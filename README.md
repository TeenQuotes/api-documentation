# Teen Quotes API
All API calls to endpoints require an **access_token**. Check the authentication section to know how to get one.

## Authentication

- **[<code>POST</code> oauth](https://github.com/TeenQuotes/api-documentation/blob/master/authentication/POST_oauth_password.md)** Request an `access_token` for a user.
- **[<code>POST</code> oauth](https://github.com/TeenQuotes/api-documentation/blob/master/authentication/POST_oauth_client_credentials.md)** Get an `access_token` that identifies an application itself.
- **[<code>POST</code> oauth](https://github.com/TeenQuotes/api-documentation/blob/master/authentication/POST_oauth_refresh_token.md)** Refresh an `access_token` from a `refresh_token`.

## Endpoints

#### Countries Resources
- **[<code>GET</code> countries](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/countries/GET_countries.md)** Get information about all countries.
- **[<code>GET</code> countries/:id](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/countries/GET_countries_id.md)** Get information about a country.

#### FavoriteQuotes Resources
- **[<code>POST</code> favorites/:id](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/favorites/POST_favorites_id.md)** Add a quote in the user's favorites.
- **[<code>DELETE</code> favorites/:id](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/favorites/DELETE_favorites_id.md)** Remove a quote from the user's favorites.

#### Quotes Resources
- **[<code>GET</code> quotes](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/quotes/GET_quotes.md)** Get information about multiples quotes.
- **[<code>POST</code> quotes](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/quotes/POST_quotes.md)** Submit a new quote.
- **[<code>GET</code> quotes/random](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/quotes/GET_quotes_random.md)** Get information about multiples quotes randomly ordered.
- **[<code>GET</code> quotes/:id](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/quotes/GET_quotes_id.md)** Get information about a single quote.
- **[<code>GET</code> quotes/favorites/:user_id](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/quotes/GET_quotes_favorites_user_id.md)** Returns information about favorites quotes for a given user ID.

#### Users Resources
- **[<code>POST</code> users](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/users/POST_users.md)** Create a new user.
- **[<code>GET</code> users/:id](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/users/GET_users_id.md)** Get information about a single user.
- **[<code>PUT</code> users/password](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/users/PUT_users_password.md)** Update the password of the user.
