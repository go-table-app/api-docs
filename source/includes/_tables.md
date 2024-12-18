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
