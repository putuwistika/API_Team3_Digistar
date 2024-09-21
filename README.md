
# Product API Documentation

## Overview

This API allows you to retrieve product data from a PostgreSQL database. It supports three main endpoints:
1. Retrieve all product data.
2. Retrieve product data with pagination using GET method.
3. Retrieve product data with pagination using POST method.

The data is loaded from the PostgreSQL database into memory at the start of the application for faster response times.

---

## Endpoints

### 1. Get All Products (Without Pagination)

**Endpoint**: `/api/all_products`  
**Method**: `GET`

**Description**:  
This endpoint returns all the product data in the database without pagination.

**Response Example**:
```json
[
    {
        "product_id": 1,
        "product_name": "Product A",
        "product_price": 50000,
        "stok": 100,
        "jumlah_terjual": 50,
        "rating": 4.5,
        "image_srcset": "image_a.jpg"
    },
    {
        "product_id": 2,
        "product_name": "Product B",
        "product_price": 75000,
        "stok": 200,
        "jumlah_terjual": 100,
        "rating": 4.7,
        "image_srcset": "image_b.jpg"
    }
]
```

### 2. Get Products with Pagination (GET)

**Endpoint**: `/api/products`  
**Method**: `GET`

**Description**:  
This endpoint returns product data with pagination. You can set the number of products per page and the page number using query parameters.

**Query Parameters**:
- `limit`: (optional) Number of products to return per page (default: 10).
- `page`: (optional) The page number to retrieve (default: 1).

**Example Request**:
```
GET /api/products?limit=10&page=2
```

**Response Example**:
```json
[
    {
        "product_id": 11,
        "product_name": "Product K",
        "product_price": 100000,
        "stok": 50,
        "jumlah_terjual": 30,
        "rating": 4.0,
        "image_srcset": "image_k.jpg"
    },
    {
        "product_id": 12,
        "product_name": "Product L",
        "product_price": 120000,
        "stok": 60,
        "jumlah_terjual": 20,
        "rating": 4.2,
        "image_srcset": "image_l.jpg"
    }
]
```

### 3. Get Products with Pagination (POST)

**Endpoint**: `/api/products`  
**Method**: `POST`

**Description**:  
This endpoint allows you to retrieve product data with pagination using a JSON body. This is useful if you want to send pagination parameters in the request body.

**Request Body**:
- `limit`: (optional) Number of products to return per page (default: 10).
- `page`: (optional) The page number to retrieve (default: 1).

**Example Request**:
```json
{
  "limit": 10,
  "page": 2
}
```

**Response Example**:
```json
[
    {
        "product_id": 21,
        "product_name": "Product U",
        "product_price": 150000,
        "stok": 100,
        "jumlah_terjual": 90,
        "rating": 4.7,
        "image_srcset": "image_u.jpg"
    },
    {
        "product_id": 22,
        "product_name": "Product V",
        "product_price": 180000,
        "stok": 120,
        "jumlah_terjual": 110,
        "rating": 4.8,
        "image_srcset": "image_v.jpg"
    }
]
```

---

## Error Handling

In case of an error, the API will return a response with an `error` key and a descriptive error message.

**Example Error Response**:
```json
{
    "error": "Invalid page number"
}
```

---

## Notes

- The data is cached in memory after the first load to improve response time.
- The API supports both GET and POST methods for pagination.
- Ensure the PostgreSQL database is accessible and the required Spark dependencies are installed.

---

## License

This project is open-source and available under the MIT License.
