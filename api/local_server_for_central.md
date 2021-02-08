# Map
- `localservers`
    - [`/localserver/v1/posts/text`](#localserverv1register)

# Schema
## Localservers
### `/localserver/v1/posts/text`
**POST** `/api/v1/community/:name/posts/text`

Create a text post for the following community. Request must be sent using `multipart/form-data`.

- `creator`: string, a username,
- `title`: string,
- `text`: string,
- `medias`: array of string, urls for the medias,

Response data: empty object

### `/api/v1/community/:name/posts/poll`
**POST** `/api/v1/community/:name/posts/poll`

Create a text post for the following community. Request must be sent using `multipart/form-data`.

- `community`: string,
- `question`: string,
- `answers`: array of string,

Response data: empty object


Response data: empty object.
# Types
Nothing