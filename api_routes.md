# API Routes

Hi! I'm your first Markdown file in **StackEdit**. If you want to learn about StackEdit, you can read me. If you want to play with Markdown, you can edit me. Once you have finished with me, you can create new files by opening the **file explorer** on the left corner of the navigation bar.

## Products

### Get all Products

Users should be able to view all Products.

- Require authentication: false
- Request
  - Method: GET
  - Route path: /api/products
  - Body: none
- Successful Response
  - Status Code: 200

### Create a Product

Users should be able to create a Product.

- Require Authentication: True
- Request

  - Method: POST
  - Route path: /api/products
  - Body:
    ```json
    {
        "name": "ProductName"
        "artist": "ArtistName"
        "description": "Description"
        "price": 3
    }
    ```

- Successful Response
  - Status Code: 201
- Error Response: Body Validation Errors
  - Status Code: 400
  - Body:
    ```json
    {
        "message": "Bad Request",
        "errors": {
            "name": "Name is required"
            "artist": "Artist is required"
            "description": "Description is required"
            "price": "Price must be a positive number"
        }
    }
    ```

### Update and Return existing Product

Users should be able to update their Product(s).

- Require Authentication: True
- Require proper Authentication: Product must belong to the user
- Request

  - Method: Put
  - Route Path: /api/products/:productId
  - Body:
    ```json
    {
        "name": "ProductName"
        "artist": "ArtistName"
        "description": "Description"
        "price": 2
    }
    ```

- Successful Response
  - Status Code: 200
- Error Response: Body Validation Errors
  - Status Code: 400
  - Body:
    ```json
    {
        "message": "Bad Request",
        "errors": {
            "name": "Name is required"
            "artist": "Artist is required"
            "description": "Description is required"
            "price": "Price must be a positive number"
        }
    }
    ```
- Error Response: Couldn't find a product by specified id
  - Status Code: 404
  - Body:
    ```json
    {
      "message": "Product couldn't be found"
    }
    ```

### Delete an existing product.

Users should be able to delete their Product(s).

- Require Authentication: True
- Require proper Authentication: Product must belong to the user
- Request

  - Method: DELETE
  - Route Path: /api/products/:productId
  - Body: None

- Successful Response
  - Status Code: 200
  - Body:
    ```json
    {
      "message": "Successfully deleted product"
    }
    ```
- Error Response: Couldn't find a product by specified id
  - Status Code: 404
  - Body:
    ```json
    {
      "message": "Spot couldn't be found"
    }
    ```

## Reviews

### Get all reviews by product's id

Users should be able to view all reviews on a Product.

- Require Authentication: False
- Request
  - Method: GET
  - Route Path: /api/products/:productId/reviews
  - Body: None
- Successful Response
  - Status Code: 200
- Error Response: Couldn't find a product by specified id

  - Status Code: 404
  - Body:
    ```json
    {
      "message": "Product couldn't be found"
    }
    ```

### Create and return a review for a product by id

Users should be able to create a review for a Product.

- Require Authentication: True
- Request

  - Method: POST
  - Route Path: /api/products/:productId/reviews
  - Body:
    ```json
    {
      "review": "Random comment"
    }
    ```

- Successful Response
  - Status Code: 201
- Error Response: Body validation errors

  - Status Code: 400
  - Body:
    ```json
    {
      "message": "Bad Request",
      "errors": {
        "review": "Review is required"
      }
    }
    ```

- Error Response: Couldn't find a product by specified id

  - Status Code: 404
  - Body:
    ```json
    {
      "message": "Product couldn't be found"
    }
    ```

- Error Response: Review from the current user already Exists for the Product

  - Status Code: 500
  - Body:
    ```json
    {
      "message": "User already has a review for this product"
    }
    ```

### Update and return an existing review

Users should be able to update their review for a Product.

- Require Authentication: True
- Request

  - Method: Put
  - Route Path: /api/reviews/:reviewId
  - Body:
    ```json
    {
      "review": "Random updated comment"
    }
    ```

- Successful Response
  - Status Code: 200
- Error Response: Body validation errors

  - Status Code: 400
  - Body:
    ```json
    {
        "message": "Bad Request",
        "errors": {
            "review": "Review is required"
            "stars": "Stars must be an integer from 1 to 5"
        }
    }
    ```

- Error Response: Couldn't find a product by specified id

  - Status Code: 404
  - Body:
    ```json
    {
      "message": "Product couldn't be found"
    }
    ```

### Delete an existing Review

Users should be able to delete their review from a Product.

- Require Authentication: True
- Request
  - Method: DELETE
  - Route Path: /api/reviews/:reviewId
  - Body: None
- Successful Response

  - Status Code: 200
  - Body:
    ```json
    {
      "message": "Successfully deleted review"
    }
    ```

- Error Response: Couldn't find a product by specified id

  - Status Code: 404
  - Body:
    ```json
    {
      "message": "Product couldn't be found"
    }
    ```

## Shopping Cart

### View all products in the cart.

Users should be able to view all products added to their cart.

- Require Authentication: True
- Request
  - Method: GET
  - Route Path: /api/cart
  - Body: None
- Successful Response
  - Status Code: 200
- Error Response: Can't find the cart

  - Status Code: 404
  - Body:
    ```json
    {
      "message": "Shopping Cart not found"
    }
    ```

### Add product to shopping cart

Users should be able to add products to their shopping cart.

- Require Authentication: True
- Request

  - Method: POST
  - Route Path: /api/cart
  - Body:
    ```json
    {
      "productId": 1
      "quantity": 2
    }
    ```

- Successful Response

  - Status Code: 200
  - Body:
    ```json
    {
      "message": "Product added to the cart"
      "cart": {
        "id": 1
        "products": [
          {
            "productId": 1,
            "name": ProdctName,
            "quantity": 2,
            "price": 2
          }
        ]
      }
    }
    ```

- Error Response: Body Validation Errors

  - Status Code: 400
  - Body:
    ```json
    {
      "message": "Shopping Cart not found"
    }
    ```

### Remove product from shopping cart

Users should be able to remove products from their shopping cart.

- Require Authentication: True
- Request
  - Method: DELETE
  - Route Path: /api/cart/:productId
  - Body: None
- Successful Response

  - Status Code: 200
  - Body:
    ```json
    {
      "message": "Product removed from Cart"
    }
    ```

- Error Response: Can't find product

  - Status Code: 404
  - Body:
    ```json
    {
      "message": "Can't find product in cart"
    }
    ```

### Perform a "transaction"

Users should be able to perform a "transaction" to complete their purchase.

- Require Authentication: True
- Request
  - Method: POST
  - Route Path: /api/cart/checkout
  - Body: None
- Successful Response

  - Status Code: 200
  - Body:
    ```json
    {
      "message": "Transaction successful"
    }
    ```

- Error Response

  - Status Code: 404
  - Body:
    ```json
    {
      "message": "Shopping Cart couldn't be found"
    }
    ```

## Wishlist

### View wishlist

Users should be able to view all of their wishlisted products.

- Require Authentication: True
- Request
  - Method: GET
  - Route Path: /api/wishlist
  - Body: None
- Successful Response
  - Status Code: 200
  - Body:

```json
{
  "wishlist": [
    {
      "productId": 1,
      "name": "ProductName",
      "price": 2
    },
    {
      "productId": 2,
      "name": "AnotherProductName",
      "price": 50
    }
  ]
}
```

### Add product to Wishlist

Users should be able to wishlisted products.

- Require Authentication: True
- Request

  - Method: POST
  - Route Path: /api/wishlist
  - Body:
    ```json
    {
      "productId": 1
    }
    ```

- Successful Response
  - Status Code: 200

### Delete product from Wishlist

Users should be able to delete products from their Wishlist.