### Create an order

**POST**

```
https://dropday.io/api/v1/orders
```

**Parameter**

| Field                                                 | Type     | Description                                                                                               |
| ----------------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------- |
| external_id                                           | String   | The external order number. We recommend that each order should have a unique order number.                |
| source                                                | String   | The source of the order. Usually the webshop name.                                                        |
| test *`optional`*                                     | Boolean  | Set this to true to make this order a test order. If not provided, it will not be considered a test order.|
| total                                                 | Number   | The total amount of the order.                                                                            |
| shipping *`optional`*                                 | Object   | Additional shipping information for the order.                                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;name *`optional`*             | String   | The name of the shipping provider (e.g., "UPS").                                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;description *`optional`*      | String   | Description of the shipping method (e.g., "Standard delivery").                                           |
| &nbsp;&nbsp;&nbsp;&nbsp;cost *`optional`*             | Number   | The shipping cost.                                                                                        |
| &nbsp;&nbsp;&nbsp;&nbsp;note *`optional`*             | String   | Additional notes or instructions for delivery.                                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;delivery_date *`optional`*    | String   | Expected delivery date (format: DD-MM-YYYY).                                                              |
| email *`optional`*                                    | String   | The email address of the receiver.                                                                        |
| shipping_address                                      | Object   | The shipping address for the order.                                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;first_name                    | String   | The firstname of the shipping address.                                                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;last_name                     | String   | The lastname of the shipping address.                                                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;company_name *`optional`*     | String   | The company name of the shipping address.                                                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;address1                      | String   | The street and housenumber of the shipping address.                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;address2 *`optional`*         | String   | Additional information about the shipping address, like apartment number.                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;postcode                      | String   | The postcode of the shipping address.                                                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;city                          | String   | The city of the shipping address.                                                                         |
| &nbsp;&nbsp;&nbsp;&nbsp;state *`optional`*            | String   | The state of the shipping address.                                                                        |
| &nbsp;&nbsp;&nbsp;&nbsp;country                       | String   | The country of the shipping address.                                                                      |
| &nbsp;&nbsp;&nbsp;&nbsp;phone *`optional`*            | Number   | The phone of the shipping address.                                                                        |
| products                                              | Object[] | Object with information about the products in the order (Array of Objects).                               |
| &nbsp;&nbsp;&nbsp;&nbsp;external_id                   | String   | The id of the product bought.                                                                             |
| &nbsp;&nbsp;&nbsp;&nbsp;ean13 *`optional`*            | Number   | The EAN of the product bought.                                                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;name                          | String   | The name or description of the product bought.                                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;reference *`optional`*        | String   | The reference or SKU of the product bought.                                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;quantity                      | Number   | The quantity of the product bought.                                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;stock_quantity *`optional`*   | Number   | The quantity of the product bought.                                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;price                         | Number   | The price of the product bought.                                                                          |
| &nbsp;&nbsp;&nbsp;&nbsp;purchase_price *`optional`*   | Number   | The price that you agreed on with your supplier/vendor                                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;image_url *`optional`*        | String   | The url of the image of the product bought.                                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;brand *`optional`*            | String   | The brand of the product bought.                                                                          |
| &nbsp;&nbsp;&nbsp;&nbsp;category *`optional`*         | String   | The category of the product bought.                                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;supplier *`optional`*         | String   | The supplier of the product bought.                                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;custom *`optional`*           | Object   | An object where you can add any key-value pair.                                                           |

**Request example**

```json
{
    "external_id": "L41223D",
    "source": "Example Shop Dot Org",
    "test": false,
    "total": 435.45,
    "shipping_cost": 4.95,
    "shipping": {
        "name": "DHL Group",
        "description": "Standard delivery",
        "cost": 4.95,
        "note": "Please not at the neighbor, the dogs eat the packages",
        "delivery_date": "07-11-2025"
    },
    "email": "info@example.org",
    "shipping_address":
    {
        "first_name": "John",
        "last_name": "Doe",
        "company_name": "Jeff",
        "address1": "Jumpstreet 23",
        "postcode": "4500",
        "city": "LA",
        "country": "US",
        "phone": "222 222"
    },
    "products": [
    {
        "external_id": "1",
        "ean13": "87235211235464",
        "name": "Pizza margerita",
        "reference": "PZZA00001",
        "quantity": 2,
        "stock_quantity": 424,
        "price": 10.99,
        "purchase_price": 5.95,
        "image_url": "https://example.org/pizza.jpg",
        "brand": "Italian",
        "category": "Pizza's",
        "supplier": "Mario",
        "custom":
        {
            "toppings": "onions, olives",
            "customer_message": "No ananas/pineapple"
        }

    },
    {
        "external_id": "2",
        "ean13": "07235211235464",
        "reference": "COKE",
        "name": "Coca Cola",
        "quantity": 2,
        "stock_quantity": 34,
        "price": 2.50,
        "image_url": "https://example.org/cola.jpg",
        "brand": "Coca Cola",
        "category": "Drinks",
        "supplier": "The Coca Cola Company",
        "custom":
        {
            "customer_message": "No ice"
        }
    }]
}
```

---

## All possible status codes


### Success 200

An HTTP status `200` is issued whenever your request was a success.

| Message              | Description                                                           |
| -------------------- | --------------------------------------------------------------------- |
| Order created        | The order is successfully created.                                    |
| Order already exists | An order with this external_id already exists for this user\/project. |


**Response**

```json
{
    "message": "Order created",
    "reference": 98
}
```

### Error 422

Sometimes a status HTTP `422` is returned. The response usually contains a field property to indicate which field is causing the issue.

For example: 


| Field                         | Description                                        |
| ----------------------------- | -------------------------------------------------- |
| external_id                   | The external id field is required.                 |
| shipping_address.firstname    | The shipping_address.firstname field is required.  |
| products.0.external_id        | The products.0.external_id field is required.      |


**Error response example**

```json
{
    "message": "Errors",
    "errors":{
        "external_id":[
            "The external id field is required."
        ],
        "shipping_address.firstname":[
            "The shipping address.firstname field is required."
        ],
        "products.0.external_id":[
            "The products.0.external_id field is required."
        ]
    }
}
```

### Error 500

Sometimes a status HTTP `500` is returned. This means that it cannot be processed and the reason is unknown. 

---

## Retrieve orders

### List all orders (paginated)

**GET**

```
https://dropday.io/api/v1/orders
```

Retrieve a paginated list of orders with optional filtering.

**Query Parameters**

| Parameter                    | Type    | Description                                                                                              |
| ---------------------------- | ------- | -------------------------------------------------------------------------------------------------------- |
| external_id *`optional`*     | String  | Filter by external order ID. Supports partial match.                                                     |
| date_from *`optional`*       | String  | Filter orders created on or after this date. ISO 8601 format (e.g., `2025-09-22T10:30:00`).              |
| date_to *`optional`*         | String  | Filter orders created on or before this date. ISO 8601 format (e.g., `2025-09-22T23:59:59`).             |
| statuses *`optional`*        | String  | Comma-separated list of statuses to filter. Values: `completed`, `partially_completed`, `failed`, `pending`, `ruled`, `declined`, `skipped`. |
| supplier_ids *`optional`*    | String  | Comma-separated list of supplier IDs to filter orders by supplier.                                       |
| total_min *`optional`*       | Number  | Filter orders with a total amount greater than or equal to this value.                                   |
| total_max *`optional`*       | Number  | Filter orders with a total amount less than or equal to this value.                                      |
| blocked *`optional`*         | Boolean | Filter by blocked status. Set to `true` to show only blocked orders, `false` for non-blocked orders.    |
| include_test *`optional`*    | Boolean | Set to `true` to include test orders in the results. Test orders are excluded by default.                |
| per_page *`optional`*        | Number  | Number of results per page. Maximum `100`, default `50`.                                                 |

**Request example (cURL)**

```bash
curl -X GET "https://dropday.io/api/v1/orders?statuses=pending,completed&date_from=2025-09-01T00:00:00&per_page=25" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -H "api-key: tdh7nNUp3DZAHsMtw3dQYhDsm3wf593hMGbyXP6Y5R8DTF2Rwy4QCvkWFYQb" \
  -H "account-id: 101"
```

**Request example with multiple filters (cURL)**

```bash
curl -X GET "https://dropday.io/api/v1/orders?external_id=ORD-2025&statuses=completed,partially_completed&supplier_ids=5,12&total_min=50&total_max=500&blocked=false&include_test=false&per_page=50" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -H "api-key: tdh7nNUp3DZAHsMtw3dQYhDsm3wf593hMGbyXP6Y5R8DTF2Rwy4QCvkWFYQb" \
  -H "account-id: 101"
```

**Response example**

```json
{
    "current_page": 1,
    "data": [
        {
            "id": 1542,
            "external_id": "ORD-2025-00142",
            "reference": "123",
            "source": "Example Shop",
            "test": false,
            "blocked": false,
            "total": 156.45,
            "shipping_address": {
                "email": "customer@example.org",
                "first_name": "Jane",
                "last_name": "Smith",
                "company_name": null,
                "phone": "+1 555 123 4567",
                "address1": "123 Main Street",
                "address2": "Apt 4B",
                "city": "New York",
                "postcode": "10001",
                "state": "NY",
                "country": "US"
            },
            "shipping": {
                "cost": 5.95,
                "name": "DHL Express",
                "description": "Next day delivery",
                "note": "Leave at front door",
                "delivery_date": "2025-09-25"
            },
            "custom": {
                "gift_wrap": true,
                "gift_message": "Happy Birthday!"
            },
            "order_lines": [
                {
                    "id": 3201,
                    "external_id": "PROD-001",
                    "name": "Wireless Headphones",
                    "ean13": "8712345678901",
                    "reference": "WH-PRO-BLK",
                    "quantity": 1,
                    "stock_quantity": 150,
                    "price": 89.99,
                    "purchase_price": 45.00,
                    "brand": "AudioTech",
                    "category": "Electronics",
                    "image_url": "https://example.org/images/headphones.jpg",
                    "custom": {
                        "color": "Black",
                        "warranty": "2 years"
                    },
                    "current_status": "completed",
                    "matched_supplier": {
                        "id": 5,
                        "name": "TechSupply Co."
                    }
                },
                {
                    "id": 3202,
                    "external_id": "PROD-002",
                    "name": "Phone Case",
                    "ean13": "8712345678902",
                    "reference": "PC-IP15-CLR",
                    "quantity": 2,
                    "stock_quantity": 500,
                    "price": 29.99,
                    "purchase_price": 12.50,
                    "brand": "CaseMaster",
                    "category": "Accessories",
                    "image_url": "https://example.org/images/phonecase.jpg",
                    "custom": null,
                    "current_status": "completed",
                    "matched_supplier": {
                        "id": 12,
                        "name": "AccessoryWorld"
                    }
                }
            ],
            "suppliers": [
                {
                    "id": 5,
                    "name": "TechSupply Co."
                },
                {
                    "id": 12,
                    "name": "AccessoryWorld"
                }
            ],
            "created_at": "2025-09-22T14:30:00.000000Z",
            "updated_at": "2025-09-23T09:15:22.000000Z"
        },
        {
            "id": 1541,
            "external_id": "ORD-2025-00141",
            "reference": "DD-98541",
            "source": "Example Shop",
            "test": false,
            "blocked": false,
            "total": 67.50,
            "shipping_address": {
                "email": "john.doe@example.com",
                "first_name": "John",
                "last_name": "Doe",
                "company_name": "Doe Enterprises",
                "phone": "+1 555 987 6543",
                "address1": "456 Oak Avenue",
                "address2": null,
                "city": "Los Angeles",
                "postcode": "90001",
                "state": "CA",
                "country": "US"
            },
            "shipping": {
                "cost": 3.50,
                "name": "Standard Shipping",
                "description": "3-5 business days",
                "note": null,
                "delivery_date": null
            },
            "custom": null,
            "order_lines": [
                {
                    "id": 3200,
                    "external_id": "PROD-003",
                    "name": "USB-C Cable 2m",
                    "ean13": "8712345678903",
                    "reference": "USBC-2M",
                    "quantity": 3,
                    "stock_quantity": 1000,
                    "price": 12.99,
                    "purchase_price": 5.00,
                    "brand": "CablePro",
                    "category": "Cables",
                    "image_url": "https://example.org/images/cable.jpg",
                    "custom": null,
                    "current_status": "pending",
                    "matched_supplier": {
                        "id": 5,
                        "name": "TechSupply Co."
                    }
                }
            ],
            "suppliers": [
                {
                    "id": 5,
                    "name": "TechSupply Co."
                }
            ],
            "created_at": "2025-09-22T10:15:00.000000Z",
            "updated_at": "2025-09-22T10:15:00.000000Z"
        }
    ],
    
    "links": {
        "first": "https://dropday.io/api/v1/orders?page=1",
        "last": "https://dropday.io/api/v1/orders?page=5",
        "prev": null,
        "next": "https://dropday.io/api/v1/orders?page=2"
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 5,
        "path": "https://dropday.io/api/v1/orders",
        "per_page": 50,
        "to": 50,
        "total": 234
    }
}
```

---

### Get a single order

**GET**

```
https://dropday.io/api/v1/orders/{reference}
```

Retrieve a single order by its reference.

**Path Parameters**

| Parameter   | Type   | Description                              |
| ----------- | ------ | ---------------------------------------- |
| reference   | String | The unique reference of the order (e.g., `123`). |

**Request example (cURL)**

```bash
curl -X GET "https://dropday.io/api/v1/orders/123" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -H "api-key: tdh7nNUp3DZAHsMtw3dQYhDsm3wf593hMGbyXP6Y5R8DTF2Rwy4QCvkWFYQb" \
  -H "account-id: 101"
```

**Response example**

```json
{
    "id": 1542,
    "external_id": "ORD-2025-00142",
    "reference": "123",
    "source": "Example Shop",
    "test": false,
    "blocked": false,
    "total": 156.45,
    "shipping_address": {
        "email": "customer@example.org",
        "first_name": "Jane",
        "last_name": "Smith",
        "company_name": null,
        "phone": "+1 555 123 4567",
        "address1": "123 Main Street",
        "address2": "Apt 4B",
        "city": "New York",
        "postcode": "10001",
        "state": "NY",
        "country": "US"
    },
    "shipping": {
        "cost": 5.95,
        "name": "DHL Express",
        "description": "Next day delivery",
        "note": "Leave at front door",
        "delivery_date": "2025-09-25"
    },
    "custom": {
        "gift_wrap": true,
        "gift_message": "Happy Birthday!"
    },
    "order_lines": [
        {
            "id": 3201,
            "external_id": "PROD-001",
            "name": "Wireless Headphones",
            "ean13": "8712345678901",
            "reference": "WH-PRO-BLK",
            "quantity": 1,
            "stock_quantity": 150,
            "price": 89.99,
            "purchase_price": 45.00,
            "brand": "AudioTech",
            "category": "Electronics",
            "image_url": "https://example.org/images/headphones.jpg",
            "custom": {
                "color": "Black",
                "warranty": "2 years"
            },
            "current_status": "completed",
            "matched_supplier": {
                "id": 5,
                "name": "TechSupply Co."
            },
            "logs": [
                {
                    "id": 12345601,
                    "status": "pending",
                    "message": "Order line created",
                    "created_at": "2025-09-22T14:30:00.000000Z"
                },
                {
                    "id": 12345602,
                    "status": "ruled",
                    "message": "Matched to supplier TechSupply Co.",
                    "created_at": "2025-09-22T14:30:05.000000Z"
                },
                {
                    "id": 12345603,
                    "status": "completed",
                    "message": "Successfully sent to supplier",
                    "created_at": "2025-09-22T14:31:12.000000Z"
                }
            ]
        },
        {
            "id": 3202,
            "external_id": "PROD-002",
            "name": "Phone Case",
            "ean13": "8712345678902",
            "reference": "PC-IP15-CLR",
            "quantity": 2,
            "stock_quantity": 500,
            "price": 29.99,
            "purchase_price": 12.50,
            "brand": "CaseMaster",
            "category": "Accessories",
            "image_url": "https://example.org/images/phonecase.jpg",
            "custom": null,
            "current_status": "completed",
            "matched_supplier": {
                "id": 12,
                "name": "AccessoryWorld"
            },
            "logs": [
                {
                    "id": 12345601,
                    "status": "pending",
                    "message": "Order line created",
                    "created_at": "2025-09-22T14:30:00.000000Z"
                },
                {
                    "id": 12345602,
                    "status": "ruled",
                    "message": "Matched to supplier AccessoryWorld",
                    "created_at": "2025-09-22T14:30:05.000000Z"
                },
                {
                    "id": 12345603,
                    "status": "completed",
                    "message": "Successfully sent to supplier",
                    "created_at": "2025-09-22T14:32:45.000000Z"
                }
            ]
        }
    ],
    "suppliers": [
        {
            "id": 5,
            "name": "TechSupply Co."
        },
        {
            "id": 12,
            "name": "AccessoryWorld"
        }
    ],
    "created_at": "2025-09-22T14:30:00.000000Z",
    "updated_at": "2025-09-23T09:15:22.000000Z"
}
```

---

## Response fields reference

### Order object

| Field                                                    | Type     | Description                                                                |
| -------------------------------------------------------- | -------- | -------------------------------------------------------------------------- |
| id                                                       | Number   | The internal unique identifier of the order.                               |
| external_id                                              | String   | The external order ID from your system.                                    |
| reference                                                | String   | The unique Dropday reference for the order.                                |
| source                                                   | String   | The source/origin of the order (e.g., webshop name).                       |
| test                                                     | Boolean  | Indicates if this is a test order.                                         |
| blocked                                                  | Boolean  | Indicates if the order is blocked from processing.                         |
| total                                                    | Number   | The total amount of the order.                                             |
| shipping_address                                         | Object   | The shipping address details.                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;email                            | String   | Email address of the recipient.                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;first_name                       | String   | First name of the recipient.                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;last_name                        | String   | Last name of the recipient.                                                |
| &nbsp;&nbsp;&nbsp;&nbsp;company_name                     | String   | Company name (if applicable).                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;phone                            | String   | Phone number of the recipient.                                             |
| &nbsp;&nbsp;&nbsp;&nbsp;address1                         | String   | Primary address line (street and house number).                            |
| &nbsp;&nbsp;&nbsp;&nbsp;address2                         | String   | Secondary address line (apartment, suite, etc.).                           |
| &nbsp;&nbsp;&nbsp;&nbsp;city                             | String   | City name.                                                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;postcode                         | String   | Postal/ZIP code.                                                           |
| &nbsp;&nbsp;&nbsp;&nbsp;state                            | String   | State or province.                                                         |
| &nbsp;&nbsp;&nbsp;&nbsp;country                          | String   | Country code (e.g., "US", "NL").                                           |
| shipping                                                 | Object   | Shipping method details.                                                   |
| &nbsp;&nbsp;&nbsp;&nbsp;cost                             | Number   | The shipping cost.                                                         |
| &nbsp;&nbsp;&nbsp;&nbsp;name                             | String   | Name of the shipping carrier/method.                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;description                      | String   | Description of the shipping method.                                        |
| &nbsp;&nbsp;&nbsp;&nbsp;note                             | String   | Additional delivery instructions.                                          |
| &nbsp;&nbsp;&nbsp;&nbsp;delivery_date                    | String   | Expected delivery date.                                                    |
| custom                                                   | Object   | Custom fields as key-value pairs.                                          |
| order_lines                                              | Object[] | Array of order line items.                                                 |
| suppliers                                                | Object[] | Array of unique suppliers for this order.                                  |
| created_at                                               | String   | ISO 8601 timestamp when the order was created.                             |
| updated_at                                               | String   | ISO 8601 timestamp when the order was last updated.                        |

### Order line object

| Field                                                    | Type     | Description                                                                |
| -------------------------------------------------------- | -------- | -------------------------------------------------------------------------- |
| id                                                       | Number   | The internal unique identifier of the order line.                          |
| external_id                                              | String   | The external product ID from your system.                                  |
| name                                                     | String   | The name/description of the product.                                       |
| ean13                                                    | String   | The EAN-13 barcode of the product.                                         |
| reference                                                | String   | The SKU or reference code of the product.                                  |
| quantity                                                 | Number   | The quantity ordered.                                                      |
| stock_quantity                                           | Number   | The available stock quantity at time of order.                             |
| price                                                    | Number   | The selling price of the product.                                          |
| purchase_price                                           | Number   | The purchase/cost price from the supplier.                                 |
| brand                                                    | String   | The brand of the product.                                                  |
| category                                                 | String   | The category of the product.                                               |
| image_url                                                | String   | URL to the product image.                                                  |
| custom                                                   | Object   | Custom fields as key-value pairs.                                          |
| current_status                                           | String   | Current status: `pending`, `ruled`, `completed`, `partially_completed`, `failed`, `declined`, `skipped`. |
| matched_supplier                                         | Object   | The supplier matched to this order line.                                   |
| &nbsp;&nbsp;&nbsp;&nbsp;id                               | Number   | The supplier's unique identifier.                                          |
| &nbsp;&nbsp;&nbsp;&nbsp;name                             | String   | The supplier's name.                                                       |
| logs                                                     | Object[] | Array of status change logs (included when fetching single order).         |

### Supplier object

| Field   | Type   | Description                           |
| ------- | ------ | ------------------------------------- |
| id      | Number | The supplier's unique identifier.     |
| name    | String | The supplier's name.                  |

---

## Error responses

### Error 401 - Unauthorized

Returned when authentication fails due to missing or invalid credentials.

**Response example**

```json
{
    "message": "Unauthorized",
    "error": "Invalid or missing api-key or account-id header"
}
```

**Common causes:**

- Missing `api-key` header
- Missing `account-id` header
- Invalid or expired API key
- Account ID does not match the API key

### Error 404 - Not Found

Returned when the requested order does not exist.

**Request example (cURL)**

```bash
curl -X GET "https://dropday.io/api/v1/orders/INVALID-REF" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -H "api-key: tdh7nNUp3DZAHsMtw3dQYhDsm3wf593hMGbyXP6Y5R8DTF2Rwy4QCvkWFYQb" \
  -H "account-id: 101"
```

**Response example**

```json
{
    "message": "Not Found",
    "error": "Order with reference 'INVALID-REF' not found"
}
```

### Error 500 - Internal Server Error

Returned when an unexpected server error occurs.

**Response example**

```json
{
    "message": "Internal Server Error",
    "error": "An unexpected error occurred. Please try again later."
}
```
