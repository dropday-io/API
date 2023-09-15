### Retrieve products

**GET**

```
https://dropday.io/api/v1/products
```

**Parameter**

This API resource is paginated due to the large amount of product that can be retrieved from this API. 100 items are displayed per page.
`?page=*`

---

## All possible status codes


### Success 200

An HTTP status `200` is given on  whenever your request was a success.


**Example response**

```json
{
    "current_page": 1,
    "data": [
        {
            "id": 336,
            "project_id": 15,
            "product_feed_id": 2,
            "sku": "A1234",
            "ean13": "84xxxxxxxxxxx",
            "name": "Product A",
            "purchase_price": 9.99,
            "stock_quantity": 8,
            "active": 1,
            "created_at": "2023-09-06T09:12:16.000000Z",
            "updated_at": "2023-09-06T09:12:27.000000Z"
        },
        ...
    ],
    "first_page_url": "https://dropday.io/api/v1/products?page=1",
    "from": 1,
    "last_page": 2,
    "last_page_url": "https://dropday.io/api/v1/products?page=2",
    "next_page_url": "https://dropday.io/api/v1/products?page=2",
    "path": "https://dropday.io/api/v1/products",
    "per_page": 100,
    "prev_page_url": null,
    "to": 100,
    "total": 105
}
```

### Error 500

In case a HTTP code `500` is returned, their 

