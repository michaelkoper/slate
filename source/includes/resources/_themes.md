# Themes

## Get all Themes

```shell
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/themes"
```

> The above command returns JSON structured like this:

```json
  {
    "id": "clean",
    "name": "Modern Theme"
  }, {
    "id": "classic",
    "name": "Classic Theme"
  }
}
```

This endpoint retrieves all available themes.

### HTTP Request

`GET https://app.nusii.com/api/v2/themes`
