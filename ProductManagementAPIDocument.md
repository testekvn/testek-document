# Product Store API

This API allows you to place a product order which will be ready for pick-up in the store.<br/>
The API is available at [`Swagger`](http://localhost/api/v0/prod-man/swagger-ui.html#) <br/>
Alternative URL: [`Swagger`](http://localhost/api/v0/prod-man/swagger-ui.html#)  (HTTP only!) <br/> 

Contact: 
- Website: [`blog.testek.vn`](http://blog.testek.vn)
- Vincent - `083.286.8822` or `info@testek.vn`
## Endpoints
<img width="812" alt="image" src="https://github.com/testekvn/testek-document/assets/59607205/d0a89419-11d1-445e-899a-299e9c53bc9b">


- [Products](#Products)
  - [Create a product](#Create-a-product)
  - [Update a product](#Update-a-product)
  - [Get all products](#Get-all-products)
  - [Get a product](#Get-a-product)
  - [Delete a product](#Delete-a-product)
- [Category](#Category)
  - [Create a category](#Create-a-category)
  - [Update a category](#Update-a-category)
  - [Get all category](#Get-all-category)
  - [Get a category](#Get-a-category)
  - [Delete a category](#Delete-a-category)
- [Supplier](#Supplier)
  - [Create a supplier](#Create-a-supplier)
  - [Update a supplier](#Update-a-supplier)
  - [Get all supplier](#Get-all-supplier)
  - [Get a supplier](#Get-a-supplier)
  - [Delete a supplier](#Delete-a-supplier)
- [Sale-employee - Developing...](#Sale-employee)
  - [Create a sale-employee](#Create-a-sale-employee)
  - [Update a sale-employee](#Update-a-sale-employee)
  - [Get all sale-employee](#Get-all-sale-employee)
  - [Get a sale-employee](#Get-a-sale-employee)
  - [Delete a sale-employee](#Delete-a-sale-employee)
- [Customer - Developing...](#Customer)
  - [Create a customer](#Create-a-customer)
  - [Update a customer](#Update-a-customer)
  - [Get all customer](#Get-all-customer)
  - [Get a customer](#Get-a-customer)
  - [Delete a customer](#Delete-a-customer)
- [Cart - Developing...](#Cart)
  - [Get a cart](#Get-a-cart)
  - [Get cart items](#Get-cart-items)
  - [Create a new cart](#Create-a-new-cart)
  - [Add an item to cart](#Add-an-item-to-cart)
  - [Modify an item in the cart](#Modify-an-item-in-the-cart)
  - [Replace an item in the cart](#Replace-an-item-in-the-cart)
  - [Delete an item in the cart](#Delete-an-item-in-the-cart)
- [Orders - Developing...](#Orders)
  - [Get all orders](#Get-all-orders)
  - [Get a single order](#Get-a-single-order)
  - [Create a new order](#Create-a-new-order)
  - [Update an order](#Update-an-order)
  - [Delete an order](#Delete-an-order)
- [API Authentication](#API-Authentication)
  - [Login with local account](#Login-with-local-account)

## Products

### Create a product
**`POST /product`**

Description: Create a product

**Parameters**

| Name        | Type   | In   | Required | Info                  | Description                                                        |
| ----------- |--------|------|----------|-----------------------|--------------------------------------------------------------------|
| `category`  | UUID   | body | Yes      |            | Specifies the category id with status ACTIVE                       |
| `supplier`  | UUID   | body | Yes      |           | Specifies the supplier id - Refer to Supplier Module               |
| `description`  | String | body | No       | Length: 255           | Specifies the decription to get more product information           |
| `name`  | String | body | Yes      | Length: 255           | Specifies the name of product                                      |
| `price`  | Double | body | Yes      |         | Specifies the product price                                        |
| `quantity`  | Number | body | Yes      |           | Specifies the number of product from the inventory                 |
| `unit`  | String | body | No       | Length: 255           | Specifies the unit of product                                      |
| `code`  | String | body | Yes      | Length: 255           | Specifies the unique code of product. The value will be uppercase automatically |

**Status codes**<br/>

| Status code              | Description                                         | 
|--------------------------|-----------------------------------------------------|
| `201 OK`                 | Indicates a successful response.                    | 
| `400 Bad Request`        | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized`       | Indicates that the token provided are invalid.      | 
| `403 Forbidden`          | Indicates that the user don't have the permission.  | 
| `404 Not Found`          | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed` | Indicates that the API method provided are invalid. | 

Example response:

```
[]
```

### Update a product

**`PUT /product/:id`**

Description: Update the value for a specific product

**Parameters**

| Name          | Type   | In   | Required | Info                  | Description                                                                    |
|---------------|--------|------|----------|-----------------------|--------------------------------------------------------------------------------|
| `id`          | UUID   | Path | Yes      |            | Specifies the id of product which you want to change value                     |
| `category`    | UUID   | body | Yes      |            | Specifies the category id with status ACTIVE                                   |
| `supplier`    | UUID   | body | Yes      |           | Specifies the supplier id - Refer to Supplier Module                           |
| `description` | String | body | No       | Length: 255           | Specifies the decription to get more product information                       |
| `name`        | String | body | Yes      | Length: 255           | Specifies the name of product                                                  |
| `price`       | Double | body | Yes      |         | Specifies the product price                                                    |
| `quantity`    | Number | body | Yes      |           | Specifies the number of product from the inventory                             |
| `unit`        | String | body | No       | Length: 255           | Specifies the unit of product                                                  |
| `code`        | String | body | Yes      | Length: 255           | Specifies the unique code of product. The value will be uppercase automatically |

**Status codes**<br/>

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 

Example response:

```
[]
```

### Get all products

**`GET /product/search`**

Returns a list of products with conditions from the inventory.

**Parameters**

| Name           | Type   | In    | Required | Info             | Description                                                                                                                                                                  |
|----------------|--------|-------|---------|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `keyword`      | String | query  | No     | Length: 255      | Specifies the searching keyword. Search by name, description.By default, all products will be displayed.                                                                     |
| `category`     | String   | query  | o      |        Length: 255          | Specifies the category name                                                                                                                                                  |
| `suppliers`    | String   | query  | No     |     Length: 255             | Specifies the supplier name                                                                                                                                                  |
| `productCodes` | String | query  | No     |    Length: 255              | Specifies the product code                                                                                                                                                   |
| `page`         | Number | query | No      | Min: 1      | Specifies the page number you want to get products                                                                                                                           |
| `limit`        | Number | query | No      | Min: 1 ; Max: 50 | Specifies the number of product for each page. Default : 50                                                                                                                  |
| `sort`     | Formate | query | No      |  | Specifies the colum name which you want to sort<br/>`+` It's ASC <br/>`-` It's DESC <br/>Example: `-productName` ~ Sort column `productName` with type `DESC`<br/> Support: `productName`, `quantity`, `suppliers`, `price` |

**Status codes**

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 
Example response:

```
[]
```

### Get a product

**`GET /product/:productId/detail`**

Returns a single product from the inventory.

**Parameters**

| Name            | Type    | In    | Required | Description                                      |
| --------------- |---------|-------| -------- | ------------------------------------------------ |
| `productId`     | UUID    | Path  | Yes      | Specifies the product's id you wish to retrieve. |

**Status codes**

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 
Example response:
```
[]
```

### Delete a product


**`DELETE /product/:productId`**

Delete a single product from the inventory.

**Parameters**

| Name            | Type    | In    | Required | Description                                                                                             |
| --------------- |---------|-------|----------|---------------------------------------------------------------------------------------------------------|
| `productId`     | UUID    | Path  | Yes      | Specifies the product's id you wish to delete.                                                          |
| `isSoft`     | boolean | query | No       | Specifies the way to delete. <br/>`true` - change the product status <br/>`false`  remove from database. |

**Status codes**

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 

Example response:
```
[]
```

## Category
### Create a category
**`POST /category`**

Description: Create a category

**Parameters**

| Name        | Type   | In   | Required | Info                  | Description                           |
| ----------- |--------|------|----------|-----------------------|---------------------------------------|
| `cateDesc`  | String   | body | No      |    Length: 255        | Specifies the category description    |
| `categoryName`  | String   | body | Yes      | Length: 255          | Specifies the category name           |
| `status`  | String | body | No       | Length: 255           | Specifies the status of this category |

**Status codes**<br/>

| Status code             | Description                                         | 
|-------------------------|-----------------------------------------------------|
| `201 OK`                | Indicates a successful response.                    | 
| `400 Bad Request`       | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized`      | Indicates that the token provided are invalid.      | 
| `403 Forbidden`         | Indicates that the user don't have the permission.  | 
| `404 Not Found`         | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed` | Indicates that the API method provided are invalid. | 

Example response:

```
[]
```

### Update a category

**`PUT /category/:id`**

Description: Update the value for a specific category

**Parameters**

| Name          | Type   | In   | Required | Info                  | Description                                                |
|---------------|--------|------|----------|-----------------------|------------------------------------------------------------|
| `id`          | UUID   | Path | Yes      |            | Specifies the id of category which you want to change value |
| `cateDesc`    | UUID   | body | Yes      |            | Specifies the category description with status ACTIVE      |
| `status`    | UUID   | body | Yes      |           | Specifies the category status                      |

**Status codes**<br/>

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 

Example response:

```
[]
```

### Get all category

**`GET /category/search`**

Returns a list of categories with conditions.

**Parameters**

| Name       | Type    | In    | Required | Info             | Description                                                                                                                                                     |
|------------|---------|-------|---------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `keyword`  | String  | query  | No     | Length: 255      | Specifies the searching keyword. Search by name, description.By default, all categories will be displayed.                                                      |
| `category` | String  | query  | o      |        Length: 255          | Specifies the category name                                                                                                                                     |
| `page`     | Number  | query | No      | Min: 1      | Specifies the page number you want to get categories                                                                                                            |
| `limit`    | Number  | query | No      | Min: 1 ; Max: 50 | Specifies the number of category for each page. Default : 50                                                                                                    |
| `sort`     | Formate | query | No      |  | Specifies the colum name which you want to sort<br/>`+` It's ASC <br/>`-` It's DESC <br/>Example: `-categoryName` ~ Sort column `categoryName` with type `DESC` |

**Status codes**

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 
Example response:

```
[]
```


### Get a category

**`GET /category/:categoryId/detail`**

Returns a single category .

**Parameters**

| Name            | Type    | In    | Required | Description                                       |
| --------------- |---------|-------| -------- |---------------------------------------------------|
| `categoryId`     | UUID    | Path  | Yes      | Specifies the category's id you wish to retrieve. |

**Status codes**

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 

### Delete a category
Delete a single category.

**`DELETE /category/:categoryId`**

**Parameters**

| Name            | Type    | In    | Required | Description                                                                                                                                        |
| --------------- |---------|-------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `categoryId`     | UUID    | Path  | Yes      | Specifies the category's id you wish to delete.                                                                                                    |
| `isSoft`     | boolean | query | No       | Specifies the way to delete. <br/> `true`  change the category status <br/>`false`  remove from database without product mapping with this category |

**Status codes**

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 



## Supplier
### Create a supplier

**`POST /supplier`**

Description: Create a supplier

**Parameters**

| Name          | Type   | In   | Required | Info        | Description                                                 |
|---------------|--------|------|----------|-------------|-------------------------------------------------------------|
| `supAddress`    | String   | body | Yes       | Length: 255 | Specifies the supplier address                              |
| `supCity`    | String   | body | No       |   Length: 255          | Specifies the supplier description with status ACTIVE       |
| `supContactName`    | String   | body | Yes       | Length: 255            | Specifies the supplier contact name                         |
| `supCountry`    | String   | body | No       |  Length: 255           | Specifies the supplier country                              |
| `supPhone`    | String   | body | Yes       | Length: 255            | Specifies the supplier phone                                |
| `supPostalCode`    | String | body | No       |  Length: 255           | Specifies the supplier postal code                          |
| `supName`    | String | body | Yes      |  Length: 255           | Specifies the supplier name                                 |

**Status codes**<br/>

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 

Example response:

```
[]
```

### Update a supplier

**`PUT /supplier/:id`**

Description: Update the value for a specific supplier

**Parameters**

| Name          | Type   | In   | Required | Info        | Description                                                 |
|---------------|--------|------|----------|-------------|-------------------------------------------------------------|
| `id`          | UUID   | Path | Yes      |             | Specifies the id of supplier which you want to change value |
| `supAddress`    | String   | body | No       | Length: 255 | Specifies the supplier address                              |
| `supCity`    | String   | body | No      |   Length: 255          | Specifies the supplier description with status ACTIVE       |
| `supContactName`    | String   | body | No      | Length: 255            | Specifies the supplier contact name                         |
| `supCountry`    | String   | body | No      |  Length: 255           | Specifies the supplier country                              |
| `supPhone`    | String   | body | No      | Length: 255            | Specifies the supplier phone                                |
| `supPostalCode`    | String | body | No      |  Length: 255           | Specifies the supplier postal code                          |

**Status codes**<br/>

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 

Example response:

```
[]
```

### Get all supplier

**`GET /supplier/search`**

Returns a list of supplier with conditions.

**Parameters**

| Name       | Type    | In    | Required | Info             | Description                                                                                                                                                     |
|------------|---------|-------|---------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `keyword`  | String  | query  | No     | Length: 255      | Specifies the searching keyword. Search by name, description.By default, all suppliers will be displayed.                                                       |
| `supplier` | String  | query  | o      |        Length: 255          | Specifies the supplier name                                                                                                                                     |
| `page`     | Number  | query | No      | Min: 1      | Specifies the page number you want to get suppliers                                                                                                             |
| `limit`    | Number  | query | No      | Min: 1 ; Max: 50 | Specifies the number of product for each page. Default : 50                                                                                                     |
| `sort`     | Formate | query | No      |  | Specifies the colum name which you want to sort<br/>`+` It's ASC <br/>`-` It's DESC <br/>Example: `-supplierName` ~ Sort column `supplierName` with type `DESC` |

**Status codes**

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 
Example response:

```
[]
```


### Get a supplier

**`GET /supplier/:supplierId/detail`**

Returns a single supplier .

**Parameters**

| Name            | Type    | In    | Required | Description                                       |
| --------------- |---------|-------| -------- |---------------------------------------------------|
| `supplierId`     | UUID    | Path  | Yes      | Specifies the supplier's id you wish to retrieve. |

**Status codes**

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 

### Delete a supplier
Delete a single supplier.

**`DELETE /supplier/:supplierId`**

**Parameters**

| Name            | Type    | In    | Required | Description                                                                                                                                        |
| --------------- |---------|-------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `supplierId`    | UUID    | Path  | Yes      | Specifies the supplier's id you wish to delete.                                                                                                    |

**Status codes**

| Status code        | Description                                         | 
|--------------------|-----------------------------------------------------|
| `200 OK`           | Indicates a successful response.                    | 
| `400 Bad Request`  | Indicates that the parameters provided are invalid. | 
| `401 Unauthorized` | Indicates that the token provided are invalid.      | 
| `403 Forbidden`    | Indicates that the user don't have the permission.  | 
| `404 Not Found`    | Indicates that the API Path provided are invalid.   | 
| `405 Method Not Allowed`  | Indicates that the API method provided are invalid. | 



## Sale-employee
### Create a sale-employee
### Update a sale-employee
### Get all sale-employee
### Get a sale-employee
### Delete a sale-employee

## Customer
### Create a customer
### Update a customer
### Get all customer
### Get a customer
### Delete a customer

## Cart

### Get a cart

**`GET /carts/:cartId`**

Returns a cart.

**Parameters**

| Name     | Type   | In   | Required | Description                                        |
| -------- | ------ | ---- | -------- | -------------------------------------------------- |
| `cartId` | string | path | Yes      | Specifies the id of the cart you wish to retrieve. |

**Status codes**

| Status code   | Description                                            |
| ------------- | ------------------------------------------------------ |
| 200 OK        | Indicates a successful response.                       |
| 404 Not found | Indicates that there is no cart with the specified id. |

### Get cart items

Returns the items in a cart.

**`GET /carts/:cartId/items`**

**Parameters**

| Name     | Type   | In   | Required | Description                                                            |
| -------- | ------ | ---- | -------- | ---------------------------------------------------------------------- |
| `cartId` | string | path | Yes      | Specifies the id of the cart for which you wish to retrieve the items. |

**Status codes**

| Status code   | Description                                            |
| ------------- | ------------------------------------------------------ |
| 200 OK        | Indicates a successful response.                       |
| 404 Not found | Indicates that there is no cart with the specified id. |

### Create a new cart

To create a new cart, submit an empty POST request to the `/carts` endpoint.

**`POST /carts`**

Creates a new cart and returns the id in the response body.

**Parameters**

No parameters are accepted for this request.

**Status codes**

| Status code | Description                                            |
| ----------- | ------------------------------------------------------ |
| 201 Created | Indicates that the cart has been created successfully. |

Example response body:

```
{
   "created": true,
   "cartId": "bx0-ycNjqIm5IvufuuZ09"
}
```

### Add an item to cart

Allows the addition of items to an existing cart. Only one item can be added at a time.

**`POST /carts/:cartId/items`**

The request body needs to be in JSON format.

**Parameters**

| Name        | Type    | In   | Required | Description                                         |
| ----------- | ------- | ---- | -------- | --------------------------------------------------- |
| `cartId`    | string  | path | Yes      | Specifies the cart id.                              |
| `productId` | string  | body | Yes      | Specifies the product id                            |
| `quantity`  | integer | body | No       | If no quantity is provided, the default value is 1. |

Example request body:

```
{
   "productId": 1234
}
```

**Status codes**

| Status code     | Description                                          |
| --------------- | ---------------------------------------------------- |
| 201 Created     | Indicates that the item has been added successfully. |
| 400 Bad Request | Indicates that the parameters provided are invalid.  |

### Modify an item in the cart

Allows modifying information about an item in the cart.

**`PATCH /carts/:cartId/items/:itemId`**

The request body needs to be in JSON format.

**Parameters**

| Name       | Type    | In   | Required | Description            |
| ---------- | ------- | ---- | -------- | ---------------------- |
| `cartId`   | string  | path | Yes      | Specifies the cart id. |
| `itemId`   | string  | path | Yes      | Specifies the item id. |
| `quantity` | integer | body | Yes      | Quantity               |

**Status codes**

| Status code     | Description                                                    |
| --------------- | -------------------------------------------------------------- |
| 204 No Content  | Indicates that the item has been updated successfully.         |
| 400 Bad Request | Indicates that the parameters provided are invalid or missing. |
| 404 Not found   | The cart or the item could not be found.                       |

### Replace an item in the cart

Replace an item in the cart.

**`PUT /carts/:cartId/items/:itemId`**

The request body needs to be in JSON format.

**Parameters**

| Name        | Type    | In   | Required | Description               |
| ----------- | ------- | ---- | -------- | ------------------------- |
| `cartId`    | string  | path | Yes      | Specifies the cart id.    |
| `itemId`    | string  | path | Yes      | Specifies the item id.    |
| `productId` | integer | body | Yes      | Specifies the product id. |
| `quantity`  | integer | body | No       | Quantity                  |

**Status codes**

| Status code     | Description                                                    |
| --------------- | -------------------------------------------------------------- |
| 204 No Content  | Indicates that the item has been updated successfully.         |
| 400 Bad Request | Indicates that the parameters provided are invalid or missing. |
| 404 Not found   | The cart or the item could not be found.                       |

### Delete an item in the cart

Deletes an item in the cart.

**`DELETE /carts/:cartId/items/:itemId`**

**Parameters**

| Name        | Type   | In   | Required | Description             |
| ----------- | ------ | ---- | -------- | ----------------------- |
| `cartId`    | string | path | Yes      | Specifies the cart id.  |
| `itemId`    | string | path | Yes      | Specifies the item id.  |

**Status codes**

| Status code    | Description                                            |
| -------------- | ------------------------------------------------------ |
| 204 No Content | Indicates that the item has been deleted successfully. |
| 404 Not found  | The cart or the item could not be found.               |

## Orders

### Get all orders

Returns all orders created by the API client.

**`GET /orders`**

**Parameters**

| Name            | Type   | In     | Required | Description                                   |
| --------------- | ------ | ------ | -------- | --------------------------------------------- |
| `Authorization` | string | header | Yes      | Specifies the bearer token of the API client. |

**Status codes**

| Status code      | Description                                                                                            |
| ---------------- | ------------------------------------------------------------------------------------------------------ |
| 200 OK           | Indicates a successful response.                                                                       |
| 401 Unauthorized | Indicates that the request has not been authenticated. Check the response body for additional details. |

### Get a single order

Returns a single order.

**`GET /orders/:orderId`**

**Parameters**

| Name            | Type    | In     | Required | Description                         |
| --------------- | ------- | ------ | -------- | ----------------------------------- |
| `Authorization` | string  | header | Yes      | The bearer token of the API client. |
| `orderId`       | string  | path   | Yes      | The order id.                       |
| `invoice`       | boolean | query  | No       | Show the PDF invoice.               |

**Status codes**

| Status code      | Description                                                                                            |
| ---------------- | ------------------------------------------------------------------------------------------------------ |
| 200 OK           | Indicates a successful response.                                                                       |
| 401 Unauthorized | Indicates that the request has not been authenticated. Check the response body for additional details. |
| 404 Not found    | Indicates that there is no order with the specified id associated with the API client.                 |

### Create a new order

**`POST /orders`**

The request body needs to be in JSON format.
Once the order has been successfully submitted, the cart is deleted.

**Parameters**

| Name            | Type   | In     | Required | Description                          |
| --------------- | ------ | ------ | -------- | ------------------------------------ |
| `Authorization` | string | header | Yes      | The bearer token of the API client.  |
| `cartId`        | string | body   | Yes      | The cart id                          |
| `customerName`  | string | body   | Yes      | The name of the customer.            |
| `comment`       | string | body   | No       | A comment associated with the order. |

Example request body:

```
{
    "cartId": "ZFe4yhG5qNhmuNyrbLWa4",
    "customerName": "John Doe"
}
```

**Status codes**

| Status code      | Description                                                                                            |
| ---------------- | ------------------------------------------------------------------------------------------------------ |
| 201 Created      | Indicates that the order has been created successfully.                                                |
| 400 Bad Request  | Indicates that the parameters provided are invalid.                                                    |
| 401 Unauthorized | Indicates that the request has not been authenticated. Check the response body for additional details. |

### Update an order

**`PATCH /orders/:orderId`**

The request body needs to be in JSON format.

**Parameters**

| Name            | Type   | In     | Required | Description                          |
| --------------- | ------ | ------ | -------- | ------------------------------------ |
| `Authorization` | string | header | Yes      | The bearer token of the API client.  |
| `orderId`       | string | path   | Yes      | The order id.                        |
| `customerName`  | string | body   | No       | The name of the customer.            |
| `comment`       | string | body   | No       | A comment associated with the order. |

**Status codes**

| Status code      | Description                                                                                            |
| ---------------- | ------------------------------------------------------------------------------------------------------ |
| 204 No Content   | Indicates that the order has been updated successfully.                                                |
| 400 Bad Request  | Indicates that the parameters provided are invalid.                                                    |
| 401 Unauthorized | Indicates that the request has not been authenticated. Check the response body for additional details. |
| 404 Not found    | Indicates that there is no order with the specified id associated with the API client.                 |

Example request body:

```
{
 "customerName": "Joe Doe"
}
```

### Delete an order

**`DELETE /orders/:orderId`**

**Parameters**

| Name            | Type   | In     | Required | Description                         |
| --------------- | ------ | ------ | -------- | ----------------------------------- |
| `Authorization` | string | header | Yes      | The bearer token of the API client. |
| `orderId`       | string | path   | Yes      | The order id.                       |

**Status codes**

| Status code      | Description                                                                                            |
| ---------------- | ------------------------------------------------------------------------------------------------------ |
| 204 No Content   | Indicates that the order has been deleted successfully.                                                |
| 400 Bad Request  | Indicates that the parameters provided are invalid.                                                    |
| 401 Unauthorized | Indicates that the request has not been authenticated. Check the response body for additional details. |
| 404 Not found    | Indicates that there is no order with the specified id associated with the API client.                 |

## API Authentication

Some endpoints may require authentication. To submit or view an order, you need to register your account and login to obtain an access token.

The endpoints that require authentication expect a bearer token sent in the `Authorization` header.

Example:

`Authorization: Bearer YOUR TOKEN`

### Login with local account

**`POST /login-with-local`**

**Parameters**

The request body needs to be in JSON format.

| Name          | Type   | In   | Required | Description       |
| ------------- | ------ | ---- | -------- |-------------------|
| `username`  | string | body | Yes      | The user name     |
| `password` | string | body | Yes      | The user password |


**Status codes**

| Status code     | Description                                                                       |
|-----------------|-----------------------------------------------------------------------------------|
| 201 Created     | Indicates that the client has been registered successfully.                       |
| 400 Bad Request | Indicates that the parameters provided are invalid.                               |
| 409 Conflict    | Indicates that an API client has already been registered with this email address. |

Example request body:

```
```

The response body will contain the access token.
