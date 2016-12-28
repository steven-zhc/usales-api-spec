FORMAT: 1A
HOST: http://localhost:5050/

# usales

USales APIs. This is USales backend services.

# Data Structures

## Message
+ message: Data not found (string)

## Category Base
+ name: toy (string)

## Category Updateable
+ name: toy (string)

## Category (Category Base)
+ cid: 1 (number) - Category ID

## Category Array (array[Category])

## Product Base
+ name: Hot Wheel (string) - Product name
+ cid: 1 (number) - Category ID
+ desc: A kind of car model (string, optional) - Product description
+ price: 3.99 (number) - List Price of a product
+ url: `http://a.b.com` (string, optional) - production offical url

## Product Updateable
+ cid: 1 (number, optional) - Category ID
+ desc: A kind of car model (string, optional) - Product description
+ price: 3.99 (number, optional) - List Price of a product
+ url: 'http://a.b.com' (string, optional) - production offical url

## Product (Product Base)
+ pid: 1 (number) - Product ID
+ cname: toy (string) - Category Name

## Product Array (array[Product])

## Line Body
+ p: 10.00 (number) - Price
+ t: 0.88 (number) - Tax
+ s: 0.00 (number) - Shipping Fee
+ d: `-1.20` (number) - Discount
+ total: 19.68 (number, optional) - Total price of this body

## Line Body Updateable
+ p: 10.00 (number, optional) - Price
+ t: 0.88 (number, optional) - Tax
+ s: 0.00 (number, optional) - Shipping Fee
+ d: `-1.20` (number, optional) - Discount

## Order Line Base
+ pid: 1 (number) - Product ID
+ q: 2 (number) - Quantity
+ model: SL33 (string, optional) - Product model
+ note: A gift for brother (string, optional) - a note of this line
+ total: 23.69 (number, optional) - Total of this line
+ profit: 3.99 (number, optional) - Profit of this line
+ purchase (Line Body)
+ sell (Line Body)

## Order Line Updateable
+ q: 2 (number, optional) - Quantity
+ model: SL33 (string, optional) - Product model
+ note: A gift for brother (string, optional) - a note of this line
+ total: 23.69 (number, optional) - Total of this line
+ profit: 3.99 (number, optional) - Profit of this line
+ purchase (Line Body Updateable, optional)
+ sell (Line Body Updateable, optional)

## Order Line (Order Line Base)
+ lid: 1 (number) - Order Line ID

## Order Line Array (array[Order Line])

## Order Header Base
+ deliverFee: 3.99 (number, optional) - Deliver fee
+ deliverDate: 2016-10-30 (string, optional) - Deliver date
+ trackingNo: US1234 (string, optional) - Tracking #
+ payment: 30.00 (number, optional) - Finally payment
+ note: A gifit for brother (string, optional) - a note of this order

## Order Base (Order Header Base)
+ lines (array[Order Line Base])

## Order (Order Header Base)
+ oid: 1 (number) - Order ID
+ status: 1 (enum[number]) - status of order
    + 0 - Deleted/Canceled
    + 1 - Inquiring
    + 2 - Processing
    + 3 - Shipping
    + 4 - Complete
+ lines (array[Order Line])

## Order Array (array[Order])

## Order Updateable (Order Header Base)

# Group Product APIs

## Category [/category]
### Create Category [POST]
Add a new Category

+ Request (application/json)
    + Attributes (Category Base)

+ Response 201 (application/json)
    + Attributes (Category)

## Category Collection [/category{?name}]
### Retrieve Categories  [GET]
Get a list of active category. Or search categories.

+ Parameters
    + name: toy (string, optional) - The name of category to search (it is case insensitive and doesn't need to match the whole name)

+ Response 200 (application/json)
    + Attributes (Category Array)

## A Category [/category/{cid}]
+ Parameters
    + cid: 1 (number) - ID of the category in form of an integer

### Retrieve a specific category [GET]
+ Response 200 (application/json)
    + Attributes (Category)

+ Response 404 (application/json)
    + Attributes (Message)
    + Body

            {
                "message": "Category not found."
            }

### Update Category [PATCH]
+ Response 200 (application/json)
    + Attributes (Category Updateable)

+ Response 404 (application/json)
    + Attributes (Message)
    + Body

            {
                "message": "Category not found."
            }

## Product [/product]
A Product is the good you could sell and purchase.
### Create Product [POST]
Add a new Product

+ Request (application/json)
    + Attributes (Product Base)

+ Response 201 (application/json)
    + Attributes (Product)

## Product Collection [/product{?name,cid}]
### Retrieve Products  [GET]
Get a list of product.

+ Parameters
    + name: toy (string, optional) - The name of Product to search (it is case insensitive and doesn't need to match the whole name)
    + cid: 1 (number, optional) - The category ID

+ Response 200 (application/json)
    + Attributes (Product Array)

## A Product [/product/{pid}]
+ Parameters
    + pid: 1 (number) - ID of the Product in form of an integer

### Retrieve a specific product [GET]
+ Response 200 (application/json)
    + Attributes (Product)

+ Response 404 (application/json)
    + Attributes (Message)
    + Body

            {
                "message": "Product not found."
            }

### Update Product [PATCH]
+ Response 200 (application/json)
    + Attributes (Product Updateable)

+ Response 404 (application/json)
    + Attributes (Message)
    + Body

            {
                "message": "Product not found."
            }

# Group Order APIs
purchase and sell request.

## Order [/order] 
### Create Order [POST]
Add a new Order

+ Request (application/json)
    + Attributes (Order Base)

+ Response 201 (application/json)
    + Attributes (Order)

## Order Collection [/order{?name,status}]
### Retrieve Orders  [GET]
Get a list of orders.

+ Parameters
    + name: toy (string, optional) - The name of Product to search (it is case insensitive and doesn't need to match the whole name)
    + status: 1 (number, optional) - The status of Order

+ Response 200 (application/json)
    + Attributes (Order Array)

## An Order [/order/{oid}]
+ Parameters
    + oid: 1 (number) - ID of the Order in form of an integer

### Retrieve a specific Order [GET]
+ Response 200 (application/json)
    + Attributes (Order)

+ Response 404 (application/json)
    + Attributes (Message)
    + Body

            {
                "message": "Order not found."
            }

### Update Order [PATCH]
+ Response 200 (application/json)
    + Attributes (Order Updateable)

+ Response 404 (application/json)
    + Attributes (Message)
    + Body

            {
                "message": "Order not found."
            }

## Order Line Collection [/order/{oid}/line]
+ Parameters
    + oid: 1 (number) - ID of the Order in form of an integer

### Retrieve Order Lines [GET]
Get a list of order lines in a specific order.
+ Response 200 (application/json)
    + Attributes (Order Line Array)

### Append a new Line [POST]
Create a new line of order
+ Request (application/json)
    + Attributes (Order Line Base)

+ Response 201 (application/json)
    + Attributes (Order Line)

## An Order Line [/order/{oid}/line/{lid}]
+ Parameters
    + oid: 1 (number) - ID of the Order in form of an integer
    + lid: 1 (number) - ID of the Order Line in form of an integer

### Update Line [PATCH]
Update an Order Line
+ Response 200 (application/json)
    + Attributes (Order Line Updateable)

+ Response 404 (application/json)
    + Attributes (Message)
    + Body

            {
               "message": "Order Line not found."
            }

### Delete Line [DELETE]
Delete an Order Line
+ Response 200 (application/json)
    + Attributes (Message)
    + Body

            {
                "message": "Sucessfully Deleted."
            }

+ Response 404 (application/json)
    + Attributes (Message)
    + Body

            {
                "message": "Order Line not found."
            }