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
- posted: `datetime` in UTC in the format `dd/mm/yy hh:mm:ss`,

Response data: empty object

### `/localserver/v1/posts/poll`
**POST** `/localserver/v1/posts/poll`

Create a poll post for the following community. Request must be sent using `multipart/form-data`.

- `creator`: string, a username,
- `question`: string,
- `answers`: array of string,
- `posted`: `datetime` in UTC in the format `dd/mm/yy hh:mm:ss`,

Response data: empty object

### `/localserver/v1/posts/:post_id/likes`
**POST** `/localserver/v1/posts/:post_id/likes`

Set count of likes and dislikes for the post with `post_id` id.

- `likes`: number,
- `dislikes`: number,

Response data: empty object.

### `/localserver/v1/posts/:post_id/comment`
**POST** `/localserver/v1/posts/:post_id/comment`

Comment the post with `post_id` id.

- `id`: string,
- `creator`: string, an username,
- `text`: string,
- `posted`: `datetime` in UTC in the format `dd/mm/yy hh:mm:ss`,

Response data: empty object.

# Types
Nothing