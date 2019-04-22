# Proposals

## Get all Proposals

```shell
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/proposals"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Proposal.list(page: 1, status: 'draft', archived: false)
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "126",
      "type": "proposals",
      "attributes": {
        "title": "Webdesign yourwebsite.com",
        "account-id": 3,
        "status": "draft",
        "public-id": "-NqDAkiqpiFLuuw",
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
        }
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
archived | false | If set to true, the result will only include archived proposals.

## Get a proposal

```shell
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/proposals/:id"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Proposal.get(100)
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "126",
    "type": "proposals",
    "attributes": {
      "title": "Webdesign yourwebsite.com",
      "account-id": 3,
      "status": "draft",
      "public-id": "-NqDAkiqpiFLuuw",
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
      }
    }
  }
}
```

This endpoint retrieves a single proposal

### HTTP Request

`GET https://app.nusii.com/api/v2/proposals/:id`


## Create a proposal

```shell
curl -X POST \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"proposal": {"client_id": 100, "title": "Webdesign yourwebsite.com"}}' \
  "https://app.nusii.com/api/v2/proposals"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Proposal.create(
  title: 'Webdesign yourwebsite.com',
  client_id: 100
)
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "126",
    "type": "proposals",
    "attributes": {
      "title": "Webdesign yourwebsite.com",
      "account-id": 3,
      "status": "draft",
      "public-id": "-NqDAkiqpiFLuuw",
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
      }
    }
  }
}
```

This will return 201 Created and the current JSON representation of the proposal if the creation was a success.

### HTTP Request

`POST https://app.nusii.com/api/v2/proposals`

### Attributes

Parameter | Mandatory | Type | Description
--------- | ------- | ----------- | -----------
title | no | String | Title of the proposal
client_id | no | ID | Client ID
client_email | no | String | Fetches the client associated with that email. It creates a new client if there is no client with that email. This is ignored when client_id is set.
document_section_title | no | String | Title of the documents section. Default: Documents
prepared_by_id | no | ID | Prepared by user
expires_at | no | DateTime | Date the proposal expires
display_date | no | DateTime | By Default the date displayed on the proposal is the sent date. This can be overwritten with the display_date
report | no | Boolean | This turns the proposal into a report. Default: false
exclude_total | no | Boolean | This excludes the total from the proposal. Default: false
exclude_total_in_pdf | no | Boolean | This excludes the total from the proposal. Default: false
theme | no | String | Theme of the proposal. Default: 'clean'

## Update a proposal

```shell
curl -X PUT \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"title": "Webdesign yourwebsite.com"}' \
  "https://app.nusii.com/api/v2/proposals/:id"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

proposal = Nusii::Proposal.get(100)
proposal.title = 'Webdesign yourwebsite.com'
proposal.save
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "126",
    "type": "proposals",
    "attributes": {
      "title": "Webdesign yourwebsite.com",
      "account-id": 3,
      "status": "draft",
      "public-id": "-NqDAkiqpiFLuuw",
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
      }
    }
  }
}
```

This will return 200 OK and the current JSON representation of the proposal if the update was a success.

### HTTP Request

`PUT https://app.nusii.com/api/v2/proposals/:id`

### Attributes

Parameter | Mandatory | Type | Description
--------- | ------- | ----------- | -----------
title | no | String | Title of the proposal
client_id | no | ID | Client ID
client_email | no | String | Fetches the client associated with that email. It creates a new client if there is no client with that email. This is ignored when client_id is set.
document_section_title | no | String | Title of the documents section. Default: Documents
prepared_by_id | no | ID | Prepared by user
expires_at | no | DateTime | Date the proposal expires
display_date | no | DateTime | By Default the date displayed on the proposal is the sent date. This can be overwritten with the display_date
report | no | Boolean | This turns the proposal into a report. Default: false
exclude_total | no | Boolean | This excludes the total from the proposal. Default: false
exclude_total_in_pdf | no | Boolean | This excludes the total from the proposal. Default: false
theme | no | String | Theme of the proposal. Default: 'clean'

## Delete a proposal

```shell
curl -X DELETE \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/proposals/:id"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

proposal = Nusii::Proposal.get(100)
proposal.destroy
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "126",
    "type": "proposals",
    "attributes": {
      "title": "Webdesign yourwebsite.com",
      "account-id": 3,
      "status": "draft",
      "public-id": "-NqDAkiqpiFLuuw",
      "prepared-by-id": 3,
      "client-id": 5,
      "sender-id": null
    }
  }
}
```

This endpoint deletes a specific proposal.

### HTTP Request

`DELETE https://app.nusii.com/api/v2/proposals/:id`

## Archive a proposal

```shell
curl -X PUT \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/proposals/:id/archive"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

# TODO not implemented yet
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "126",
    "type": "proposals",
    "attributes": {
      "title": "Webdesign yourwebsite.com",
      "account-id": 3,
      "status": "draft",
      "public-id": "-NqDAkiqpiFLuuw",
      "prepared-by-id": 3,
      "client-id": 5,
      "sender-id": null,
      "archived-at": "2019-01-01T10:00:00.000Z"
    }
  }
}
```

This endpoint deletes a specific proposal.

### HTTP Request

`DELETE https://app.nusii.com/api/v2/proposals/:id`

## Send a proposal

```shell
curl -X PUT \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  -d '{"email": "your_client@email.com", "subject": "Your Proposal"}' \
  "https://app.nusii.com/api/v2/proposals/:id/send_proposal"
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

# TODO not implemented yet
```

> The above command returns JSON structured like this:

```json
{
  "status": "pending",
  "sent_at": "2017-11-10T15:04:07.037Z",
  "sender_id": null,
  "sender_name": null
}
```

This will return 200 OK and the current JSON representation.

### HTTP Request

`PUT https://app.nusii.com/api/v2/proposals/:id/send_proposal`

### Attributes

Parameter | Mandatory | Type | Description
--------- | ------- | ----------- | -----------
email | yes | String | Email of the client
cc | no | String | CC Email receipients. Need to be comma separated if contains multiple emails.
bcc | no | String | BCC Email receipients. Need to be comma separated if contains multiple emails.
subject | no | String | Subject of the email
message | no | String | Body of the email
save_email_template | no | Boolean | Overwrite email template. Default: false
sender_id | no | ID | ID of the sender
sender_email | no | String | Fetches the Sender associated with that email. This is ignored when sender_id is set.
