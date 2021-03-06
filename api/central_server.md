# Map
- `users`
    - [`/api/v1/users/register`](#apiv1usersregister)
    - [`/api/v1/users/auth`](#apiv1usersauth)
    - [`/api/v1/users/reset_request`](#apiv1usersreset_request)
    - [`/api/v1/users/reset`](#apiv1users/reset)
    - [`/api/v1/users/avatar`](#apiv1usersavatar)
    - [`/api/v1/users/about`](#apiv1usersabout)
    - [`/api/v1/users/:user_id/communities`](#apiv1userscommunities)
    - [`/api/v1/users/:user_id/subscribes`](#apiv1userssubscribes)
    - [`/api/v1/users/subscribe`](#apiv1userssubscribe)
    - [`/api/v1/users/unsubscribe`](#apiv1usersunsubscribe)
- `community`
    - [`/api/v1/community/:name`](#apiv1communityname)
    - [`/api/v1/community/:name/posts/text`](#apiv1communitynamepoststext)
    - [`/api/v1/community/:name/posts/poll`](#apiv1communitynamepostspoll)
    - [`/api/v1/community/:name/posts/:post_id`](#apiv1communitynamepostspost_id)
    - [`/api/v1/community/:name/posts/:post_id/like`](#apiv1communitynamepostspost_idlike)
    - [`/api/v1/community/:name/posts/:post_id/dislike`](#apiv1communitynamepostspost_iddislike)
    - [`/api/v1/community/:name/posts/:post_id/comment`](#apiv1communitynamepostspost_idcomment)
    - [`/api/v1/community/:name/posts/:post_id/comment/:comment_id`](#apiv1communitynamepostspost_idcommentcomment_id)
- Types
    - [`User`](#User)
    - [`Community`](#Community)
    - [`PostInfo`](#PostInfo)

# Schema
## Users
### `/api/v1/users/register`
**POST** `/api/v1/users/register`

Register a user.

- `username`: string
- `password`: string
- `email`: string

Response data: [`User`](#User)

### `/api/v1/users/auth`
**POST** `/api/v1/users/auth`

Authorize a user. Returns the token which is must be put in the `Authorization` header like this: `Authorization: bearer <token>`.

- `username`: string
- `password`: string

Response data: 
```
{
  "user": User,
  "token": "abcd1234",
}
```

### `/api/v1/users/reset_request`
**POST** `/api/v1/users/reset_request`

Sends link for the restore the password.

- `email`: string,

Response data: nothing

### `/api/v1/users/reset`
**POST** `/api/v1/users/reset`

Reset the password.

- `password`: string,
- `token`: string,

Response data: nothing

### `/api/v1/users/avatar`
**POST** `/api/v1/users/avatar`

Add an avatar to the self. The request sends using `multipart/form-data`.

- `image`: blob.

Response data: empty object

### `/api/v1/users/about`
**POST** `/api/v1/users/about`

Sets information in the "about" field.

- `about`: string,

Response data: empty object

### `/api/v1/users/:user_id/communities`
**GET** `/api/v1/users/:user_id/subscribes`

Get communities where `user_id` is owner.

Response data: `array` of [`Community`](#Community)

### `/api/v1/users/:user_id/subscribes`
**GET** `/api/v1/users/:user_id/subscribes`

Get user subscribes.

Response data: `array` of [`Community`](#Community)

### `/api/v1/users/subscribe`
**POST** `/api/v1/users/subscribe`

Subscribe to the specified community.

- `community`: string

Response data: empty object

### `/api/v1/users/unsubscribe`
**POST** `/api/v1/users/unsubscribe`

Unsubscribe from the specified community.

- `community`: string.

Response data: empty object

### `/api/v1/users/:user/posts`
**GET** `/api/v1/users/:user/posts?page=N&count=M`

Get M posts at the N page with.

Response data: array of [`PostInfo`](#PostInfo)

## Community
### `/api/v1/community/:name`
**GET** `/api/v1/community/:name`

Returns info about the community.

Response data: [`Community`](#Community)

### `/api/v1/community/:name/posts/text`
**POST** `/api/v1/community/:name/posts/text`

Create a text post for the following community. Request must be sent using `multipart/form-data`.

- `community`: string,
- `title`: string,
- `text`: string,
- `media`: number, count of the media files,
- `mediaN`: blob, where N - index of the media, 

Response data: empty object

### `/api/v1/community/:name/posts/poll`
**POST** `/api/v1/community/:name/posts/poll`

Create a text post for the following community. Request must be sent using `multipart/form-data`.

- `community`: string,
- `question`: string,
- `answers`: array of string,

Response data: empty object

### `/api/v1/community/:name/posts/:post_id`
**GET** `/api/v1/community/:name/post/:post_id`

Get info about post with `post_id` id.

Response data: [`PostInfo`](#PostInfo)

### `/api/v1/community/:name/posts/:post_id/like`
**POST** `/api/v1/community/:name/posts/:post_id/like`

Like the post with `post_id` id in the `name` community.

Response data: empty object.

### `/api/v1/community/:name/posts/:post_id/dislike`
**POST** `/api/v1/community/:name/posts/:post_id/dislike`

Dislike the post with `post_id` id in the `name` community.

Response data: empty object.

### `/api/v1/community/:name/posts/:post_id/comment`
**POST** `/api/v1/community/:name/posts/:post_id/comment`

Comment the post with `post_id` id in the `name` community.

- `text`: string

Response data: empty object.

### `/api/v1/community/:name/posts/:post_id/comment/:comment_id`
**GET** `/api/v1/community/:name/posts/:post_id/comment/:comment_id`

Get info about the the comment with `comment_id` of the post with `post_id` id in the `name` community.

Response data: [`CommentInfo`](#CommentInfo).

### `/api/v1/community/:name/posts/:post_id/report_hash`
**POST** `/api/v1/community/:name/posts/:post_id/report_hash`

Report that hash does not match the post. If is it, server returns `matches: false`, else `matches: true`. 

Response data: 
```json
{
  "matches": bool
}
```

# Types
## User
- username: `string`,
- avatar: `string|null`,
- karma: `number`,
- lang: `string`,
- follows: `number`,
- followers: `number`,
- registration: `date` (UTC) in format DD/MM/YY

Example:
```json
{
  "username": "Andrey",
  "avatar": null,
  "karma": -10,
  "lang": "ru",
  "follows": 30,
  "followers": 3,
  "registration": "10/02/21"
}
```

## Community
- name: `string`, slug,
- owner: `string`, username,
- title: `string`,
- avatar: `string|null`,
- address: `string`, address of the community,
- registration: date (UTC) in format DD/MM/YY,
- followers: `number`, count of the followers,

Example:
```json
{
  "name": "College_Server",
  "owner": "Otradskaya",
  "title": "Paradise on the Earth",
  "avatar": null,
  "address": "server.od.ua/api",
  "registration": "10/02/21",
  "followers": 59,
}
```

## PostInfo
- owner: `string`,
- community: `string`,
- id: `string`, an unique identifier for the post,
- hash: `string`, the hash of the title+body+author,
- liked: `bool`, true if the user like this post

Example:
```json
{
  "owner": "Otradskaya",
  "community": "College_Server",
  "id": "the_best_college",
  "hash": "sdfhy24q3gyb35hg5b",
  "liked": true,
}
```

## CommentInfo
- id: `string`,
- owner: `string`,
- hash: `string`,

Example:
```json
{
  "id": "aabb", 
  "owner": "Otradskaya",
  "hash": "sdfhy24q3gyb35hg5b",
}
```