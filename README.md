# Cloud Computing
# Tamantic API

This repository contains the backend code for the Tamantic Marketplace, a platform where users can register, log in, and manage products. The backend is built using Node.js and Firebase Firestore, with JWT for authentication and TensorFlow.js for image classification.

## Table of Contents
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Endpoints](#endpoints)
  - [User Management](#user-management)
  - [Product Management](#product-management)
  - [Image Classification](#image-classification)
  - [Product Recommendations](#product-recommendations)
- [Docker Support](#docker-support)
- [Middleware](#middleware)
- [License](#license)
  
## Features

- **User Registration**: Register users with name, email, phone, password, and profile image URL.
- **User Login**: Authenticate users and generate JWT tokens.
- **Product Management**: Create, retrieve, and search products.
- **Image Classification**: Classify product images using TensorFlow.js.
- **Recommendations**: Recommend products based on categories.


## Requirements
- Node.js
- Google Cloud SDK (gcloud) installed and configured
- Google Cloud Firestore and Google Cloud Storage enabled in Google Cloud Console
- Firebase
- TensorFlow.js for Node

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

3. **Setup Environment Variables:**

    Create a `.env` file in the root directory and add the required environment variables as described in the [Configuration](#configuration) section.

---

## Configuration
1. Create a `.env` file in the project root with the following variables:

```plaintext
PRODUCT_BUCKET_NAME='image-product-tamantic'
MARKET_BUCKET_NAME='image-market-tamantic'
USER_BUCKET_NAME='image-user-tamantic'
JWT_SECRET='tamantic'
MODEL_BUCKET_NAME='https://storage.googleapis.com/model-storage-tamantic/model.json'
MODEL_RECOMMENDATION_NAME='https://storage.googleapis.com/recommender-system-tamantic/model.json'
```

- `PRODUCT_BUCKET_NAME`: Google Cloud Storage bucket for product images.
- `MARKET_BUCKET_NAME`: Google Cloud Storage bucket for market images.
- `USER_BUCKET_NAME`: Google Cloud Storage bucket for user images.
- `JWT_SECRET`: Secret key for JWT authentication.
- `MODEL_BUCKET_NAME`: URL for the image classification model.
- `MODEL_RECOMMENDATION_NAME`: URL for the product recommendation model.

2. Ensure you have the appropriate Google Cloud credentials and access to Firestore and Storage.

## Usage

1. **Start the server:**

    ```bash
    npm run start
    ```

2. **Access the API** using [Postman](https://www.postman.com/) or any API client at `http://localhost:3000`.

---

## Endpoints
API Base URL
The API endpoints are hosted at: https://tamantic-api-fciqhbrq7a-et.a.run.app


### User Management
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
      "imageUrl" : "https://example.com/user-image.jpg"
    
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
        "imageUrl": "https://example.com/user-image.jpg",
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
      "password": "xyz1@1",
      "registerDate": "2023-05-28T00:00:00.000Z",
      "updatedDate": "2023-05-28T00:00:00.000Z",
      "imageUrl": "https://storage.googleapis.com/user-bucket/user-image.jpg"
    },
    ...
    ]
    }
    ```

### Product Management
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
      "productImageUrl": "https://example.com/product-image.jpg",
      "marketImageUrl": "https://example.com/market-image.jpg"
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

- **Search Product By Name**
  - **URL:** `/product/search`
  - **Method:** `POST`
  - **Body:**
    ```json
    {
      "name": "Product Name"
    }
    ```
  - **Response:**
    ```json
    {
    "data": [
      {
        "id": "unique-product-id",
        "product_id": 1,
        "name": "product name",
        "image": "https://example.com/product.jpg",
        "imageMarket": "https://example.com/market.jpg",
        "owner": "John Doe",
        "alamat": "Address",
        "phone": 6281234567890,
        "rate": 4.5,
        "sold": 10,
        "stock": 50,
        "price": 1000.0,
        "postdate": "2023-01-01T00:00:00.000Z",
        "categories": ["categories1", "categories2"],
        "description": "Product description"
      },
      ...
    ],
    "recommendation": [
      {
        "id": "unique-product-id",
        "product_id": 2,
        "name": "another product",
        "image": "https://example.com/another_product.jpg",
        "imageMarket": "https://example.com/another_market.jpg",
        "owner": "Jane Doe",
        "alamat": "Another Address",
        "phone": 6281234567891,
        "rate": 4.0,
        "sold": 5,
        "stock": 100,
        "price": 2000.0,
        "postdate": "2023-01-02T00:00:00.000Z",
        "categories": ["electronics", "gadgets"],
        "description": "Another product description"
      }
      ...
    ]
            

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
### Image Classification
- **Classify Image**
  - **URL:** `/predict`
  - **Method:** `POST`
  - **Body:**
    ```json
    {
      "image": "base64-encoded-image"
    }
    ```
  - **Response:**
    ```json
    {
      "result": "Label",
      "explanation": "Explanation",
      "confidenceScore": 98.76
    }
    ```
### Product Recommendations

The recommendation system uses a pre-trained model accessible via the URL specified in `MODEL_RECOMMENDATION_NAME` to recommend products based on categories similar to the searched products. This feature is automatically triggered in the [Search Products by Name](#search-products-by-name) endpoint.


## Docker Support

To build and run the project using Docker:

1. Build the Docker image:

   ```bash
   docker build -t e-commerce-api .
   ```

2. Run the Docker container:

   ```bash
   docker run -p 3000:3000 e-commerce-api
   ```

This will start the API server in a Docker container accessible at `http://localhost:3000`.

    

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
