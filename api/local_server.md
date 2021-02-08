# Schema
## `/api/v1/posts`
**GET** `/api/v1/posts?page=N&count=M`

Get M posts at the N page for the community.

Response data: array of [`PostInfo`](#PostInfo)

## `/api/v1/posts/:post_id`
**GET** `/api/v1/posts/:post_id`

Get info about post with `:post_id`.

Response data: [`Post`](#Post)

## `/api/v1/posts/:post_id/comments`
**GET** `/api/v1/posts/:post_id/comments?page=N&count=M`

Get M comments at the N page for the post.

Response data: `array` of [`Comment`](#Comment)

# Types
## PostInfo
- title: `string`,
- owner: `string`,
- likes: `number`,
- dislikes: `number`,
- type: `"text"|"poll"`
- posted: `datetime` in UTC in the format `dd/mm/yy hh:mm:ss`,

Example:
```json
{
  "title": "Title",
  "owner": "Andrey",
  "likes": 10,
  "dislikes": 20,
  "type": "text",
  "posted": "10/02/21"
}
```

## Post
- title: `string`,
- owner: `string`,
- likes: `number`,
- dislikes: `number`,
- type: `"text"|"post"`,
- kind: [`TextPostKind`](#TextPostKind)`|`[`PollPostKind`](#PollPostKind)
- posted: `datetime` in UTC in the format `dd/mm/yy hh:mm:ss`,

Example:
```json
{
  "title": "Title",
  "owner": "Andrey",
  "likes": 10,
  "dislikes": 20,
  "type": "text",
  "kind": {
    "text": "some",
    "media": []
  },
  "posted": "10/02/21 10:58:48"
}
```

## TextPostKind
- text: `string`,
- media: `array` of `string` - urls of the photos, up to 10 elements,
Example:
```json
{
  "text": "Lorem ipsum",
  "media": [
      "link.to/photo1",
      "link.to/photo2",
  ] 
}
```

## PollPostKind
- question: `string`,
- answers: `array` of [`PollAnswer`](#PollAnswer)
Example:
```json
{
  "question": "Lorem ipsum",
  "answers": [
      {
          "text": "answer1",
          "voter_count": 10
      },
  ] 
}
```

## PollAnswer
- text: `string`,
- `voter_count`: `number`
Example:
```json
{
  "text": "answer",
  "voter_count": 0
}
```

## Comment
- id: `number`,
- owner: `string`,
- text: `string`,
- posted: `datetime` in UTC in the format `dd/mm/yy hh:mm:ss`,

Example:
```json
{
  "id": 123,
  "owner": "Andrey",
  "text": "some",
  "posted": "10/02/21"
}