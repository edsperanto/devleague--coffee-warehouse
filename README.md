# Coffee Warehouse API Reference

A restful API used to help serve and manage data of coffee at a warehouse. The API server will be built using postgres, node, express, and sequelize. All responses will be in JSON format. All successful requests will be answered with a JSON containing `{"success": true}`. All failed requests will be answered with a JSON containing `{"success": false}` and the key `"reason"` containing the reason (string) for the failed request.

## Database Schema

### location

| **Property** | **Data Type** | **Unit** |
|---|---|---|
| id **(primary)** | serial number | --- |
| name | string | --- |
| capacity | integer | bags |
| used_capacity | integer | bags |
| remaining_capacity | integer | bags |

### coffee

| **Property** | **Data Type** | **Unit** |
|---|---|---|
| id **(primary)** | serial number | --- |
| name | string | --- |
| brand | string | --- |
| caffeine | integer | mg/L |
| price | currency | USD |
| location_id **(foreign)** | integer | --- |

### order

| **Property** | **Data Type** | **Unit** |
|---|---|---|
| id **(primary)** | serial number | --- |
| order_date | date (yyyy-mm-dd) | GMT |
| order_time | time (hh:mm:ss) | GMT |
| total_price | currency | USD |
| status | enum('pending', 'shipped', 'voided') | --- |
| payment_id **(foreign)** | integer | --- |
| customer_id **(foreign)** | integer | --- |

### customer

| **Property** | **Data Type** | **Unit** |
|---|---|---|
| id **(primary)** | serial number | --- |
| first_name | string | --- |
| last_name | string | --- |
| full_name | string | --- |
| company | string | --- |
| address | integer | --- |
| phone | phone | --- |
| email | email | --- |
| tenure | integer | years |

### payment

| **Property** | **Data Type** | **Unit** |
|---|---|---|
| id **(primary)** | serial number | --- |
| type | enum('credit', 'debit', 'checking') | --- |
| card_number | integer | --- |
| expiration | date(yyyy-mm) | GMT |
| bank | string | --- |
| routing_number | integer | --- |
| account_number | integer | --- |

### order_coffee (join)

| **Property** | **Data Type** | **Unit** |
|---|---|---|
| id **(primary)** | serial number | --- |
| amount | integer | bags |
| subtotal | currency | USD |
| order_id **(foreign)** | integer | --- |
| coffee_id **(foreign)** | integer | --- |

### customer_order (join)

| **Property** | **Data Type** |
|---|---|
| id **(primary)** | serial number |
| customer_id **(foreign)** | integer |
| order_id **(foreign)** | integer |

### customer_payment (join)

| **Property** | **Data Type** |
|---|---|
| id **(primary)** | serial number |
| customer_id **(foreign)** | integer |
| payment_id **(foreign)** | integer |

## Routes Overview

### Aggregate Data

Aggregate data requests are obtained via the `/all` route. 

| **HTTP Method** | **URL** | **Response** | **Action** |
|---|---|---|---|---|
| `GET` | `/all/locations` | `{"locations": [array]}` | Get list of all warehouse locations. |
| `GET` | `/all/coffees` | `{"coffees": [array]}` | Get list of all coffee types. |
| `GET` | `/all/orders` | `{"orders": [array]}` | Get list of all customer orders. |
| `GET` | `/all/customers` | `{"customers": [array]}` | Get list of all customer information. |

### Location Data

Location data requests are obtained via the `/location` route.

| **HTTP Method** | **URL** | **Response** | **Action** |
|---|---|---|---|---|
| `GET` | `/location/:id` | `{"location": { data }}` | Get all data related to a location by its ID. |
| `POST` | `/location/new` | `{"location": { data }}` | Creates a new location entry, and responds with an object containing all data related to the newly created location. |
| `PUT` | `/location/:id` | `{"location": { data }}` | Change data related to a location by its ID, and responds with an object containing all data related to the edited location. |
| `DELETE` | `/location/:id` | `{"success": true}` | Delete a location. |

### Coffee Data

Coffee data requests are obtained via the `/coffee` route.

| **HTTP Method** | **URL** | **Response** | **Action** |
|---|---|---|---|---|
| `GET` | `/coffee/:id` | `{"coffee": { data }}` | Get all data related to a coffee type by its ID. |
| `POST` | `/coffee/new` | `{"coffee": { data }}` | Creates a new coffee type entry, and responds with an object containing all data related to the newly created coffee type. |
| `PUT` | `/coffee/:id` | `{"coffee": { data }}` | Change data related to a coffee by its ID, and responds with an object containing all data related to the edited coffee type. |
| `DELETE` | `/coffee/:id` | `{"success": true}` | Delete a coffee type. |

### Order Data

Order data requests are obtained via the `/order` route.

| **HTTP Method** | **URL** | **Response** | **Action** |
|---|---|---|---|---|
| `GET` | `/order/:id` | `{"order": { data }}` | Get all data related to an order by its ID. |
| `POST` | `/order/new` | `{"order": { data }}` | Creates a new order entry, and responds with an object containing all data related to the newly created order. |
| `PUT` | `/order/:id` | `{"order": { data }}` | Change data related to an order by its ID, and responds with an object containing all data related to the edited order. |
| `DELETE` | `/order/:id` | `{"success": true}` | Delete an order. |

### Customer Data

Customer data requests are obtained via the `/customer` route.

| **HTTP Method** | **URL** | **Response** | **Action** |
|---|---|---|---|---|
| `GET` | `/customer/:id` | `{"customer": { data }}` | Get all data related to a customer by its ID. |
| `POST` | `/customer/new` | `{"customer": { data }}` | Creates a new customer entry, and responds with an object containing all data related to the newly created customer. |
| `PUT` | `/customer/:id` | `{"customer": { data }}` | Change data related to a customer by its ID, and responds with an object containing all data related to the edited customer. |
| `DELETE` | `/customer/:id` | `{"success": true}` | Delete a customer. |