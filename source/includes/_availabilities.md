# Availability

## Get Restaurant Availability

```shell
curl "https://gotable.app/api/v1/restaurants/<restaurant_id>/availability?from=2024-10-29&till=2024-11-01" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE"
```

```ruby
require 'go_table'

api = GoTable::API.new(api_key: 'YOUR_API_KEY_HERE')
restaurant = api.restaurants.find(restaurant_id)
availabilities = restaurant.availability.from('2024-10-29').till('2024-11-01')
```

> The above command returns JSON structured like this:

```json
{
  "from": "2024-09-18",
  "till": "2024-09-23",
  "availabilities": [
    {
      "date": "2024-09-18",
      "closed": false,
      "timeslots": [
        {
          "timeslot": "11:00",
          "minimum": 0,
          "maximum": 20
        },
        {
          "timeslot": "11:30",
          "minimum": 0,
          "maximum": 20
        },
        {
          "timeslot": "12:00",
          "minimum": 0,
          "maximum": 20
        }
      ]
    },
    {
      "date": "2024-09-18",
      "closed": false,
      "timeslots": [
        {
          "timeslot": "11:00",
          "minimum": 0,
          "maximum": 20
        },
        {
          "timeslot": "11:30",
          "minimum": 0,
          "maximum": 20
        },
        {
          "timeslot": "12:00",
          "minimum": 0,
          "maximum": 20
        }
      ]
    }
  ]
}
```

This endpoint retrieves the availability for a specific restaurant over a given date range.

### HTTP Request

`GET https://gotable.app/api/v1/restaurants/<restaurant_id>/availability`

### URL Parameters

| Parameter       | Description                                           |
| --------------- | ----------------------------------------------------- |
| restaurant_id\* | The ID of the restaurant to retrieve availability for |

### Query Parameters

| Parameter       | Default  | Description                                      |
| --------------- | -------- | ------------------------------------------------ |
| from            | today    | Start date for availability (format: YYYY-MM-DD) |
| till            | tomorrow | End date for availability (format: YYYY-MM-DD)   |

### Response Structure

The response includes the following main elements:

- `from`: The start date of the requested availability range
- `till`: The end date of the requested availability range
- `availabilities`: An array of availability objects, one for each date in the range

Each availability object contains:

- `date`: The date for this availability entry
- `closed`: A boolean that returns wether or not the restaurant is closed on this date.
- `timeslots`: An array of time slot objects, where each object contains:
  - `timeslot`: The time in "HH:MM" format
  - `minimum`: The minimum number of seats available at this time
  - `maximum`: The maximum number of seats available at this time
