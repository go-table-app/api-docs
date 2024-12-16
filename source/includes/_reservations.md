# Reservations

## List Restaurant Reservations

Returns a paginated list of reservations for your restaurant.

### Response Format

| Field         | Type    | Description                                                                       |
| ------------- | ------- | --------------------------------------------------------------------------------- |
| id            | integer | Unique reservation identifier                                                     |
| guest_name    | string  | Customer's name                                                                   |
| guest_email   | string  | Customer's email                                                                  |
| date          | string  | Reservation date (YYYY-MM-DD)                                                     |
| time          | string  | Reservation time (HH:MM)                                                          |
| guests        | integer | Number of guests                                                                  |
| state         | string  | Reservation status: "pending", "confirmed", "checked_in", "rejected", "cancelled" |
| restaurant_id | integer | Restaurant identifier                                                             |

### Pagination

The response includes a `meta` object with pagination details:

| Field        | Type    | Description                  |
| ------------ | ------- | ---------------------------- |
| current_page | integer | Current page number          |
| per_page     | integer | Number of items per page     |
| total_pages  | integer | Total number of pages        |
| total_count  | integer | Total number of reservations |

### Example Request

```shell
curl -X GET \
  "http://gotable.test/api/v1/restaurants/{restaurant_id}/reservations" \
  -H "Authorization: Bearer {your_api_key}" \
  -H "Content-Type: application/json"
```

```ruby
api = GoTableAPI::API.new(api_key: 'YOUR_API_KEY_HERE')
reservation = api.reservations(restaurantUid).list
```

> The above command returns JSON structured like this:

```json
{
   "reservations":[
      {
         "id":3781327,
         "guest_name":"John Doe2",
         "guest_email":"john@example.com",
         "date":"2024-11-01",
         "time":"19:00",
         "guests":4,
         "state":"pending",
         "restaurant_id":130170
      },
      {
         "id":3781328,
         "guest_name":"John Doe2",
         "guest_email":"john@example.com",
         "date":"2024-11-01",
         "time":"19:00",
         "guests":4,
         "state":"rejected",
         "restaurant_id":130170
      },
      // ... more reservations
      ],
   "meta":{
      "current_page":1,
      "per_page":20,
      "total_pages":1,
      "total_count":16
   }
}
```

## Get Reservation

```shell
curl "https://gotable.app/api/v1/restaurants/<restaurantUid>/reservations/<reservationUid>" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE"
```

```ruby
api = GoTableAPI::API.new(api_key: 'YOUR_API_KEY_HERE')
reservation = api.reservations(restaurantUid).get(reservationUid)
```

> The above command returns JSON structured like this:

```json
{
  "id": 3781341,
  "guest_name": "John Doe",
  "guest_email": "john@example.com",
  "date": "2024-12-01",
  "time": "19:00",
  "guests": 4,
  "state": "pending",
  "restaurant_id": 130170
}
```

This endpoint retrieves information about a specific reservation. Linked to a restaurant that is registered to your API Key.

### HTTP Request

`GET https://gotable.app/api/v1/<restaurantUid>/reservation/<reservationUid>`

### URL Parameters

| Parameter        | Description                      |
| ---------------- | -------------------------------- |
| restaurantUid\*  | The unique id of the restaurant  |
| reservationUid\* | The unique id of the reservation |

## Create Reservation

```shell
curl -X POST "https://gotable.app/api/v1/restaurants/<restaurantUid>/reservations" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE" \
  -H "Content-Type: application/json" \
  -d '{
    "reservation": {
      "date": "2024-11-01",
      "time": "19:00",
      "guests": 4,
      "guest_name": "John Doe",
      "guest_email": "john@example.com",
      "guest_phone": "+31612345678",
      "type": "WalkIn"
    }
  }'
```

```ruby
api = GoTableAPI::API.new(api_key: 'YOUR_API_KEY_HERE')
reservation = api.reservations(restaurantUid).create(
  date: '2024-12-01',
  time: '19:00',
  guests: 4,
  guest_name: 'John Doe',
  guest_email: 'john@example.com'
)
```

> The above command returns JSON structured like this:

```json
{
  "id": 3781341,
  "guest_name": "John Doe",
  "guest_email": "john@example.com",
  "date": "2024-12-01",
  "time": "19:00",
  "guests": 4,
  "state": "pending",
  "restaurant_id": 130170
}
```

Creates a new reservation for your restaurant. Your API key must be registered to the restaurant.

### Required Parameters

| Parameter           | Type    | Description                      |
| ------------------- | ------- | -------------------------------- |
| guest_name          | string  | Customer's name                  |
| guest_mobile        | string  | Customer's phone number          |
| guest_email         | string  | Customer's email address         |
| guests              | integer | Number of guests                 |
| duration_in_minutes | integer | Length of reservation in minutes |

### Optional Parameters

| Parameter | Type   | Description                                                                                                                                             |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| date      | string | Reservation date (YYYY-MM-DD). Required for regular reservations                                                                                        |
| time      | string | Reservation time (HH:MM). Required for regular reservations                                                                                             |
| type      | string | Set to "WalkIn" for walk-in reservations (current customers). For walk-ins, date/time default to current if not provided. Omit for regular reservations |

### HTTP Request

`POST https://gotable.app/api/v1/<restaurantUid>/reservations`

### URL Parameters

| Parameter       | Description                     |
| --------------- | ------------------------------- |
| restaurantUid\* | The unique id of the restaurant |

## Update Reservation

```shell
curl -X PUT "https://gotable.app/api/v1/restaurants/129946/reservations/12345" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE" \
  -H "Content-Type: application/json" \
  -d '{
    "reservation": {
      "guests": 5
    }
  }'
```

```ruby
api = GoTableAPI::API.new(api_key: 'YOUR_API_KEY_HERE')
api.reservations(restaurantUid).update(reservationUid, { guests: 5 })
```

> The above command returns JSON structured like this:

```json
{
  "id": 3042496,
  "guest_name": "John Doe",
  "guest_email": "customer@example.com",
  "date": "2024-11-01",
  "time": "19:00",
  "guests": 5,
  "state": "pending",
  "restaurant_id": 129946
}
```

This endpoint updates the details of a reservation.

### HTTP Request

`PUT https://gotable.app/api/v1/<restaurantUid>/reservation/<uid>`

### URL Parameters

| Parameter       | Description           |
| --------------- | --------------------- |
| restaurantUid\* | id of the restaurant  |
| uid\*           | id of the reservation |

## Cancel Reservation

```shell
curl -X PUT "https://gotable.app/api/v1/restaurants/<restaurantUid>/reservations/<reservationUid>" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE"
```

```ruby
api = GoTableAPI::API.new(api_key: 'YOUR_API_KEY_HERE')
api.reservations(restaurantUid).cancel(reservationUid)
```

> The above command returns JSON structured like this:

```json
{
  "id": 3781341,
  "guest_name": "John Doe",
  "guest_email": "john@example.com",
  "date": "2024-12-01",
  "time": "19:00",
  "guests": 5,
  "state": "pending",
  "restaurant_id": 130170
}
```

This endpoint cancels a specific reservation.

### HTTP Request

`PUT https://gotable.app/api/v1/<restaurantUid>/reservation/<uid>`

### URL Parameters

| Parameter       | Description                      |
| --------------- | -------------------------------- |
| restaurantUid\* | The unique id of the restaurant  |
| uid\*           | The unique id of the reservation |