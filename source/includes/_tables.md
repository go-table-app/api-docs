# Tables

## Get Available Restaurant Tables

```shell
curl "https://gotable.app/api/v1/restaurants/129946/tables" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE"
```

```javascript
const restaurant_id = 123456
const token = 'YOUR_API_KEY_HERE'

fetch(`https://gotable.app/api/v1/restaurants/${restaurant_id}/tables`, {
  method: 'GET',
  headers: {
    'Authorization': `Bearer ${token}`,
    'Content-Type': 'application/json'
  }
}).then(
  (response) => response.json()
).then((json) => {
  console.log('tables', json.tables)
})
```

```ruby
require 'go_table'

api = GoTable::API.new(api_key: 'YOUR_API_KEY_HERE')
restaurant = api.restaurants.find(restaurant_id)
tables = restaurant.tables
```

> The above command returns JSON structured like this:


```json
{
  "tables": [
    {
      "id": 123,
      "restaurant_id": 12345,
      "label": "Window Table",
      "section": "Main Floor",
      "preference_order": 1,
      "enabled": true,
      "realtime": true,
      "minimum_guests": 2,
      "maximum_guests": 6,
      "created_at": "2024-11-14T13:37:49.811Z",
      "updated_at": "2024-11-14T13:37:49.811Z"
    },
    {
      "id": 124,
      "restaurant_id": 12345,
      "label": "Corner Table",
      "section": "Main Floor",
      "preference_order": 1,
      "enabled": true,
      "realtime": true,
      "minimum_guests": 2,
      "maximum_guests": 6,
      "created_at": "2024-11-26T09:00:47.930Z",
      "updated_at": "2024-11-26T09:00:47.930Z"
    },
    {
      "id": 125,
      "restaurant_id": 12345,
      "label": "Corner Table",
      "section": "Back",
      "preference_order": 1,
      "enabled": true,
      "realtime": true,
      "minimum_guests": 0,
      "maximum_guests": 4,
      "created_at": "2024-11-07T09:08:56.729Z",
      "updated_at": "2024-11-07T09:08:56.729Z"
    }
  ]
}
```
This endpoint retrieves the list of tables for a restaurant.

### HTTP Request

`GET https://gotable.app/api/v1/<restaurant_id>/tables`

### URL Parameters

| Parameter       | Description                     |
| --------------- | ------------------------------- |
| restaurant_id\* | The unique id of the restaurant |

### Response body attributes

| Attribute             | Type    | Description                                               |
| --------------------- | ------- | --------------------------------------------------------- |
| label                 | string  | The name or label of the table                            |
| section               | string  | The section or area where the table is located            |
| maximum_guests        | integer | The maximum number of guests the table can accommodate    |
| minimum_guests        | integer | The minimum number of guests required for this table      |
| realtime              | boolean | Whether the table is available for realtime bookings      |
| preference_order      | integer | The order of preference for assigning this table          |
| enabled               | boolean | Whether the table is currently enabled for bookings       |
| external_table_number | string  | An external identifier for the table                      |
