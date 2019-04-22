---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Nusii API! You can use our API to access Nusii API endpoints. All endpoints URLs begin with `https://app.nusii.com/api/v2/`. All requests must be serialized in JSON and Nusii uses the [jsonapi.org](http://jsonapi.org/) specification.


# Authentication

> We offer a token based authentication. You can find your API access token [here](https://app.nusii.com). Tokens need to be added in the HTTP_AUTHORIZATION header as `Token token=your_access_token`


```shell
# With shell, you can just pass the correct header with each request
curl "app.nusii.com/api/v2/proposals"
  -H "Authorization: Token token=your_access_token"
```

> Make sure to replace `your_access_token` with your API key.

Nusii expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Token token=your_access_token`

<aside class="notice">
You must replace <code>your_access_token</code> with your personal API key.
</aside>

# Proposals

## Get All Proposals

```shell
curl "https://app.nusii.com/api/v2/proposals"
  -H "Authorization: Token token=your_access_token"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "126",
      "type": "proposals",
      "attributes": {
        "title": "Testing Videos",
        "account-id": 3,
        "status": "draft",
        "public-id": "-NqDkHbE7FLuuw",
        "prepared-by-id": 3,
        "client-id": 5,
        "sender-id": null
      }, 
      "relationships": {
        "sections": {
          "data": [
            {
              "id": "414",
              "type": "sections"
            }
          ]
        },
      }
    }
  ],
  "meta": {
    "current-page": 2,
    "next-page": 3,
    "prev-page": 1,
    "total-pages": 4,
    "total-count": 89
  }
}
```

This endpoint retrieves all proposals.

### HTTP Request

`GET https://app.nusii.com/api/v2/proposals`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
status | null | If not set retrieves all proposals, Possible states are `draft`, `pending`, `accepted`, `rejected`, or `clarification`
status | false | If set to true, the result will only include archived proposals.
page | 1 | returns the current page
page_size | 25 | size of the page

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>


# Kittens

## Get All Kittens


```shell
curl "https://app.nusii.com/api/v2/kittens"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET https://app.nusii.com/api/v2/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```shell
curl "https://app.nusii.com/api/v2/kittens/2"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten


```shell
curl "https://app.nusii.com/api/v2/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

