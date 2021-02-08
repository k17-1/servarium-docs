# Map
- `localservers`
    - [`/localserver/v1/register`](#localserverv1register)

# Schema
## Localservers
### `/localserver/v1/register`
**POST** `/localserver/v1/register`

Register a new localserver. Must be send using `multipart/form-data`.

- `name`: string, slug,
- `token`: string, user token,
- `title`: string,
- `avatar`: optional, blob, an image,

Response data: empty object.
# Types
Nothing