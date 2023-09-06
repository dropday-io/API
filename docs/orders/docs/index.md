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
| shipping_cost                                         | Number   | The total shipping cost of the order.                                                                     |
| email                                                 | String   | The email address of the receiver.                                                                        |
| shipping_address                                      | Object   | The shipping address for the order.                                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;first_name                    | String   | The firstname of the shipping address.                                                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;last_name                     | String   | The lastname of the shipping address.                                                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;company_name *`optional`*     | String   | The company name of the shipping address.                                                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;address1                      | String   | The street and housenumber of the shipping address.                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;address2 *`optional`*         | String   | Additional information about the shipping address, like apartment number.                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;postcode                      | String   | The postcode of the shipping address.                                                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;city                          | String   | The city of the shipping address.                                                                         |
| &nbsp;&nbsp;&nbsp;&nbsp;state *`optional`*            | String   | The state of the shipping address.                                                                      |
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
| &nbsp;&nbsp;&nbsp;&nbsp;image_url *`optional`*        | String   | The url of the image of the product bought.                                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;brand *`optional`*            | String   | The brand of the product bought.                                                                          |
| &nbsp;&nbsp;&nbsp;&nbsp;category *`optional`*         | String   | The category of the product bought.                                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;supplier *`optional`*         | String   | The supplier of the product bought.                                                                       |

**Request example**

```json
{
  "external_id": "L41223D",
  "source": "Example Shop Dot Org",
  "test": false,
  "total": 435.45,
  "shipping_cost": 4.95,
  "email": "info@example.org",
  "shipping_address": {
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
      "image_url": "https://example.org/pizza.jpg",
      "brand": "Italian",
      "category": "Pizza's",
      "supplier": "Mario"    
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
      "supplier": "The Coca Cola Company" 
    }
  ] 
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

