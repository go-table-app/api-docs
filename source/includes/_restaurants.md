# Restaurants

## Get Registered Restaurants

```shell
curl "https://gotable.app/api/v1/restaurants" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE"
```

```ruby
require 'go_table'

api = GoTable::API.new(api_key: 'YOUR_API_KEY_HERE')
restaurants = api.restaurants
```

> The above command returns JSON structured like this:

```json
{
  "restaurants": [
    {
      "id": 130170,
      "name": "Test Restaurant",
      "telephone": "+31 6 28 79 68 88",
      "email": "info@gotable.app",
      "street": "Brugstraat 1",
      "zipcode": "6131AC",
      "city": "Sitard",
      "country_code": "NL"
    }
  ],
  "meta": {
    "current_page": 1,
    "per_page": 20,
    "total_pages": 1,
    "total_count": 1
  }
}
```

This endpoint retrieves all restaurants registered to your API Key.

### HTTP Request

`GET https://gotable.app/api/v1/restaurants`

### Query Parameters

| Parameter | Default | Description                    |
| --------- | ------- | ------------------------------ |
| page      | 1       | The page number for pagination |
| per_page  | 20      | Number of restaurants per page |

## Get a Specific Restaurant

```shell
curl "https://gotable.app/api/v1/restaurants/<restaurant_id>" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE"
```

```javascript
const restaurant_id = 123456
const token = 'YOUR_API_KEY_HERE'

fetch(`https://gotable.app/api/v1/restaurants/${restaurant_id}`, {
  method: 'GET',
  headers: {
    'Authorization': `Bearer ${token}`,
    'Content-Type': 'application/json'
  }
}).then(
  (response) => response.json()
).then((json) => {
  console.log('restaurant data', json)
})
```

```ruby
require 'go_table'

api = GoTable::API.new(api_key: 'YOUR_API_KEY_HERE')
restaurant = api.restaurants.find(restaurant_id)
```

> The above command returns JSON structured like this:

```json
{
  "id": 130170,
  "name": "Test Restaurant",
  "telephone": "+31 6 28 79 68 88",
  "email": "info@gotable.app",
  "street": "Brugstraat 1",
  "zipcode": "6131AC",
  "city": "Sittard",
  "country_code": "NL"
}
```

This endpoint retrieves a specific restaurant.

### HTTP Request

`GET https://gotable.app/api/v1/restaurants/<restaurant_id>`

### URL Parameters

| Parameter       | Description                     |
| --------------- | ------------------------------- |
| restaurant_id\* | The unique id of the restaurant |

### Response attributes

| Attribute                       | Type    | Default  | Description                                                                     |
| ------------------------------- | ------- | -------- | ------------------------------------------------------------------------------- |
| name\*                          | string  |          | The name of the restaurant                                                      |
| email\*                         | string  |          | The email address of the restaurant                                             |
| telephone                       | string  |          | The telephone number of the restaurant                                          |
| private_feedback_url            | string  |          | URL for private feedback (must start with http:// or https://)                  |
| reservation_follow_up_setting\* | string  | 'never'  | Must be one of: 'always', 'local', 'self', or 'never'                           |
| minimum_guests                  | integer |          | Minimum number of guests allowed (must be less than or equal to maximum_guests) |
| maximum_guests                  | integer |          | Maximum number of guests allowed                                                |
| realtime_setting\*              | string  | 'off'    | Must be one of: 'off', 'availability', or 'capacity'                            |
| realtime_reject_setting\*       | string  | 'accept' | Must be one of: 'accept' or 'reject'                                            |
| country_code\*                  | string  | 'NL'     | Two-letter country code                                                         |
| maintainer_ids                  | array   |          | Array of maintainer IDs                                                         |
