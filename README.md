
# Product API Documentation

## Overview

This API allows you to retrieve product data from a PostgreSQL database and Machine Learning Model with Python. It supports three main endpoints:
1. Retrieve all product data.
2. Retrieve product data with pagination using GET method.
3. Retrieve product data with pagination using POST method.
4. Retrieve product data with products_id using GET method.
5. Retrieve product data with products_id using POST method.
6. Get Similar Products (Recomendations) by Product ID using GET method.
7. Get Best Product from AI analysis

The data is loaded from the PostgreSQL database into memory at the start of the application for faster response times.


Untuk melakukan Testing menggunakan Postman berikut [Postman.json](postman.json) yang dapat digunakan
[Postman.json](postman.json)


---
## Daftar Endpoint

### 1. Get All Products (Tanpa Pagination)

**Endpoint**: `/api/all_products`

**Method**: `GET`

**Deskripsi**: Mengambil semua produk dari database tanpa menggunakan pagination.

#### Cara Penggunaan:
```bash
GET http://localhost:5000/api/all_products
```

#### Response Contoh:
```json
[
    {
        "product_id": "8365736d-599d-4489-a262-8dc270afeba6",
        "product_name": "Product 1",
        "product_price": 15000,
        "stok": 50,
        "jumlah_terjual": 100,
        "rating": 4.5,
        "image_srcset": "image1.jpg",
        "kategori": "Kategori A"
    },
    {
        "product_id": "1234567-599d-4489-a262-8dc270afeba6",
        "product_name": "Product 2",
        "product_price": 25000,
        "stok": 20,
        "jumlah_terjual": 50,
        "rating": 4.0,
        "image_srcset": "image2.jpg",
        "kategori": "Kategori B"
    }
]
```

---

### 2. Get Products with Pagination (GET Method)

**Endpoint**: `/api/products`

**Method**: `GET`

**Deskripsi**: Mengambil daftar produk dengan pagination menggunakan query parameter `limit` dan `page`.

#### Cara Penggunaan:
```bash
GET http://localhost:5000/api/products?limit=5&page=1
```

#### Query Parameters:
- `limit`: Jumlah produk yang ingin diambil (default: 10)
- `page`: Halaman data yang ingin diambil (default: 1)

#### Response Contoh:
```json
[
    {
        "product_id": "8365736d-599d-4489-a262-8dc270afeba6",
        "product_name": "Product 1",
        "product_price": 15000,
        "stok": 50,
        "jumlah_terjual": 100,
        "rating": 4.5,
        "image_srcset": "image1.jpg",
        "kategori": "Kategori A"
    }
]
```

---

### 3. Get Products with Pagination (POST Method)

**Endpoint**: `/api/products`

**Method**: `POST`

**Deskripsi**: Mengambil daftar produk dengan pagination menggunakan `limit` dan `page` yang dikirimkan melalui body JSON.

#### Cara Penggunaan:
```bash
POST http://localhost:5000/api/products
```

#### Body Request:
```json
{
    "limit": 5,
    "page": 1
}
```

#### Response Contoh:
```json
[
    {
        "product_id": "8365736d-599d-4489-a262-8dc270afeba6",
        "product_name": "Product 1",
        "product_price": 15000,
        "stok": 50,
        "jumlah_terjual": 100,
        "rating": 4.5,
        "image_srcset": "image1.jpg",
        "kategori": "Kategori A"
    }
]
```

---

### 4. Get Product by ID (GET Method)

**Endpoint**: `/api/products/<product_id>`

**Method**: `GET`

**Deskripsi**: Mengambil detail produk berdasarkan `product_id`.

#### Cara Penggunaan:
```bash
GET http://localhost:5000/api/products/8365736d-599d-4489-a262-8dc270afeba6
```

#### Response Contoh:
```json
{
    "product_id": "8365736d-599d-4489-a262-8dc270afeba6",
    "product_name": "Product 1",
    "product_price": 15000,
    "stok": 50,
    "jumlah_terjual": 100,
    "rating": 4.5,
    "image_srcset": "image1.jpg",
    "kategori": "Kategori A",
    "brand": "Brand 1",
    "min_pembelian": 1,
    "berat_satuan": 200,
    "dimensi_ukuran": "10x10x10",
    "dikirim_dari": "Jakarta",
    "penjual": "Penjual 1",
    "description": "Deskripsi produk 1"
}
```

---

### 5. Get Product by ID (POST Method)

**Endpoint**: `/api/products_id`

**Method**: `POST`

**Deskripsi**: Mengambil detail produk berdasarkan `product_id` yang dikirimkan melalui body JSON.

#### Cara Penggunaan:
```bash
POST http://localhost:5000/api/products_id
```

#### Body Request:
```json
{
    "product_id": "8365736d-599d-4489-a262-8dc270afeba6"
}
```

#### Response Contoh:
```json
{
    "product_id": "8365736d-599d-4489-a262-8dc270afeba6",
    "product_name": "Product 1",
    "product_price": 15000,
    "stok": 50,
    "jumlah_terjual": 100,
    "rating": 4.5,
    "image_srcset": "image1.jpg",
    "kategori": "Kategori A",
    "brand": "Brand 1",
    "min_pembelian": 1,
    "berat_satuan": 200,
    "dimensi_ukuran": "10x10x10",
    "dikirim_dari": "Jakarta",
    "penjual": "Penjual 1",
    "description": "Deskripsi produk 1"
}
```

---

### 6. Get Similar Products by Product ID

**Endpoint**: `/api/product_similarity/<product_id>`

**Method**: `GET`

**Deskripsi**: Mengambil daftar produk yang mirip berdasarkan `product_id` menggunakan perhitungan cosine similarity.

#### Cara Penggunaan:
```bash
GET http://localhost:5000/api/product_similarity/8365736d-599d-4489-a262-8dc270afeba6
```

#### Response Contoh:
```json
[
    {
        "product_id": "1234567-599d-4489-a262-8dc270afeba6",
        "product_name": "Product 2",
        "product_price": 25000,
        "stok": 20,
        "jumlah_terjual": 50,
        "rating": 4.0,
        "image_srcset": "image2.jpg",
        "kategori": "Kategori B",
        "cosine_similarity": 0.85
    },
    {
        "product_id": "7890123-599d-4489-a262-8dc270afeba6",
        "product_name": "Product 3",
        "product_price": 30000,
        "stok": 15,
        "jumlah_terjual": 70,
        "rating": 4.8,
        "image_srcset": "image3.jpg",
        "kategori": "Kategori C",
        "cosine_similarity": 0.82
    }
]
```

### 7. Get Best Product from AI analysis

**Endpoint**: `/api/ai-best-products`

**Method**: `POST`

**Deskripsi**: Endpoint ini digunakan untuk mengirim daftar `product_id` ke server dan menerima rekomendasi produk terbaik berdasarkan analisis AI. AI akan memilih produk terbaik dari daftar yang diberikan berdasarkan kriteria yang telah ditentukan, seperti popularitas, relevansi, atau faktor lain yang diukur oleh algoritma.

#### Cara Penggunaan:
```bash
POST http://localhost:5000/api/ai-best-products
```

#### Body Request:
```json
{
    "product_ids": [
        "9bf12451-5274-438a-8d3f-26772d4564a6",
        "9555ced5-5d30-4e7c-b592-d4bbb1a3e049"
    ]
}

```
#### Response Contoh:
```json
{
    "comparison_result": "Hallo Digistar!\n\nBerikut adalah hasil analisis produk-produk yang dibandingkan:\n\n**MICROWAVE OVEN MODENA MG 2516 100% ORI Free OngKir seJakarta (Produk A)**\n* Keunggulan:\na. Garansi resmi produk selama 1 tahun untuk service dan sparepart, serta 2 tahun untuk magnetron.\nb. Fitur yang lengkap seperti touch control panel, child lock, dan interior light.\nc. Kapasitas oven 25 Liter yang besar.\n* Kekurangan:\na. Harga yang relatif lebih mahal (Rp 3.909.000).\nb. Dimensi produk yang besar (55x40x60cm).\nc. Berat volume produk yang besar (22.00kg).\n\n**BEKO MGB25332BG MICROWAVE AND GRILL 100% ORI Free OngKir seJakarta (Produk B)**\n* Keunggulan:\na. Harga yang relatif lebih murah (Rp 3.601.000).\nb. Dimensi produk yang lebih kecil (60x40x40cm).\nc. Berat volume produk yang lebih ringan (16.00kg).\n* Kekurangan:\na. Garansi resmi produk hanya 1 tahun untuk service dan sparepart.\nb. Fitur yang kurang lengkap dibandingkan dengan Produk A.\nc. Kapasitas oven 25 Liter yang sama dengan Produk A.\n\nSaya rekomendasikan **BEKO MGB25332BG MICROWAVE AND GRILL 100% ORI Free OngKir seJakarta** Untuk anda beli Karena harga yang lebih murah dan dimensi produk yang lebih kecil.\n\nTerima Kasih, Jangan Lupa Checkout"
}
```

---

## Error Handling

All endpoints will return a JSON response with an error message in case of failure or invalid input. For example:
```json
{
  "error": "Product not found"
}
```


---

## Teknologi yang Digunakan
- **Flask**: Web framework untuk Python.
- **PySpark**: Library untuk pemrosesan data besar dengan Spark.
- **PostgreSQL**: Database untuk menyimpan data produk.

---

---

## Notes

- The data is cached in memory after the first load to improve response time.
- The API supports both GET and POST methods for pagination.
- Ensure the PostgreSQL database is accessible and the required Spark dependencies are installed.

---

