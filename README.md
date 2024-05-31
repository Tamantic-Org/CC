# CC
# Tamantic API

Tamantic API is a backend API that provides user registration, login, user management, and product management with image support. The API uses Google Cloud Firestore for data storage and Google Cloud Storage for image storage.

## Table of Contents
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Server](#running-the-server)
- [Endpoints](#endpoints)
  - [User](#user)
  - [Product](#product)
- [Middleware](#middleware)
- [License](#license)

## Requirements
- Node.js
- Google Cloud SDK (gcloud) installed and configured
- Google Cloud Firestore and Google Cloud Storage enabled in Google Cloud Console

## Installation
1. Clone this repository:
    ```bash
    git clone https://github.com/username/tamantic-api.git
    cd tamantic-api
    ```

2. Install dependencies:
    ```bash
    npm install
    ```

## Configuration
1. Create a `.env` file in the root directory and add your Google Cloud configuration:
    ```plaintext
    GOOGLE_APPLICATION_CREDENTIALS=path/to/your/credentials.json
    ```

2. Ensure you have the appropriate Google Cloud credentials and access to Firestore and Storage.

## Running the Server
To run the server, use the following command:
```bash
node server.js
```
The server will run at `http://localhost:3000`.

## Endpoints
API Base URL
The API endpoints are hosted at: https://tamantic-api-fciqhbrq7a-et.a.run.app


### User
- **Register User**
  - **URL:** `/register`
  - **Method:** `POST`
  - **Body:**
    ```json
    {
      "name": "Name",
      "email": "email@example.com",
      "phone": "+6281234567890",
      "password": "password",
      "userImage" : "image (tipe file)"
    
    }
    ```
  - **Response:**
    ```json
    {
    "id": "user-id",
    "name": "Name",
    "email": "email@example.com",
    "phone": "81234567890",
    "registerDate": "2023-05-28T00:00:00.000Z",
    "updatedDate": "2023-05-28T00:00:00.000Z",
    "imageUrl": "https://storage.googleapis.com/user-bucket/user-image.jpg",
    "isOwner": false
    }
    ```

- **Login User**
  - **URL:** `/login`
  - **Method:** `POST`
  - **Body:**
    ```json
    {
      "email": "email@example.com",
      "password": "password"
    }
    ```
  - **Response:**
    ```json
    {
      "msg": "success",
      "result": {
        "id": "user-id",
        "name": "Name",
        "phone": "81234567890",
        "email": "email@example.com",
        "token": "jwt-token"
      }
    }
    ```

- **Get User By ID**
  - **URL:** `/users/:id`
  - **Method:** `GET`
  - **Response:**
    ```json
    {
    "id": "user-id",
    "name": "Name",
    "email": "email@example.com",
    "phone": "81234567890",
    "registerDate": "2023-05-28T00:00:00.000Z",
    "updatedDate": "2023-05-28T00:00:00.000Z",
    "imageUrl": "https://storage.googleapis.com/user-bucket/user-image.jpg",
    "isOwner": false
    }
    ```

- **Get All Users**
  - **URL:** `/users`
  - **Method:** `GET`
  - **Response:**
    ```json
    {
    "data": [
    {
      "id": "user-id",
      "name": "Name",
      "phone": "81234567890",
      "registerDate": "2023-05-28T00:00:00.000Z",
      "imageUrl": "https://storage.googleapis.com/user-bucket/user-image.jpg"
    },
    ...
    ]
    }
    ```

### Product
- **Create Product**
  - **URL:** `/product`
  - **Method:** `POST`
  - **Body:**
    ```json
    {
      "name": "Product Name",
      "owner": "Owner Name",
      "alamat": "Address",
      "phone": "081234567890",
      "rate": "4.5",
      "price: 1000,
      "sold": "100",
      "categories": "category1,category2",
      "description": "Product description",
      "productImage": "file",
      "marketImage": "file"
    }
    ```
  - **Response:**
    ```json
    {
      "data": [
        {
          "id": "product-id",
          "name": "Product Name",
          "image": "https://storage.googleapis.com/image-product-tamantic/product-image.jpg",
          "imageMarket": "https://storage.googleapis.com/image-market-tamantic/market-image.jpg",
          "owner": "Owner Name",
          "alamat": "Address",
          "phone": "81234567890",
          "price":"1000",
          "rate": 4.5,
          "sold": 100,
          "postdate": "2023-05-28T00:00:00.000Z",
          "categories": ["category1", "category2"],
          "description": "Product description"
        }
      ]
    }
    ```

- **Get Product By ID**
  - **URL:** `/products/:id`
  - **Method:** `GET`
  - **Response:**
    ```json
    {
      "data": [
        {
          "id": "product-id",
          "name": "Product Name",
          "image": "https://storage.googleapis.com/image-product-tamantic/product-image.jpg",
          "imageMarket": "https://storage.googleapis.com/image-market-tamantic/market-image.jpg",
          "owner": "Owner Name",
          "alamat": "Address",
          "phone": "81234567890",
          "rate": 4.5,
          "sold": 100,
          "postdate": "2023-05-28T00:00:00.000Z",
          "categories": ["category1", "category2"],
          "description": "Product description"
        }
      ]
    }
    ```

- **Get Products By Owner**
  - **URL:** `/user/owner/product/:owner`
  - **Method:** `GET`
  - **Response:**
    ```json
    {
      "data": [
        {
          "id": "product-id",
          "name": "Product Name",
          "image": "https://storage.googleapis.com/image-product-tamantic/product-image.jpg",
          "imageMarket": "https://storage.googleapis.com/image-market-tamantic/market-image.jpg",
          "owner": "Owner Name",
          "alamat": "Address",
          "phone": "81234567890",
          "rate": 4.5,
          "sold": 100,
          "postdate": "2023-05-28T00:00:00.000Z",
          "categories": ["category1", "category2"],
          "description": "Product description"
        }
      ]
    }
    ```

- **Get Products By Category**
  - **URL:** `/category/categories/product/:category`
  - **Method:** `GET`
  - **Response:**
    ```json
    {
      "data": [
        {
          "id": "product-id",
          "name": "Product Name",
          "image": "https://storage.googleapis.com/image-product-tamantic/product-image.jpg",
          "imageMarket": "https://storage.googleapis.com/image-market-tamantic/market-image.jpg",
          "owner": "Owner Name",
          "alamat": "Address",
          "phone": "81234567890",
          "rate": 4.5,
          "sold": 100,
          "postdate": "2023-05-28T00:00:00.000Z",
          "categories": ["category1", "category2"],
          "description": "Product description"
        }
      ]
    }
    ```

## Get All Products

**Endpoint:** `/products`

**Method:** `GET`

**Condition:** If everything is OK and products exist in the database.

**Code:** `200 OK`

**Content example:**

```json
{
    "data": [
        {
            "id": "1",
            "name": "Product 1",
            "image": "https://example.com/product1.jpg",
            "imageMarket": "https://example.com/market1.jpg",
            "owner": "Owner 1",
            "alamat": "Address 1",
            "phone": 1234567890,
            "rate": 4.5,
            "sold": 100,
            "postdate": "2022-01-01T00:00:00.000Z",
            "categories": ["Category 1", "Category 2"],
            "description": "Description 1"
        },
        {
            "id": "2",
            "name": "Product 2",
            "image": "https://example.com/product2.jpg",
            "imageMarket": "https://example.com/market2.jpg",
            "owner": "Owner 2",
            "alamat": "Address 2",
            "phone": 2345678901,
            "rate": 4.0,
            "sold": 200,
            "postdate": "2022-02-02T00:00:00.000Z",
            "categories": ["Category 3", "Category 4"],
            "description": "Description 2"
        }
    ]
}
```
## Middleware
- **Handle Invalid Method**
  - Returns a 405 response if an HTTP method is not allowed on a specific endpoint.
  - **Response:**
    ```json
    {
      "message": "Error: Method not allowed"
    }
    ```

## License
This project is licensed under the [Tamantic](LICENSE).
