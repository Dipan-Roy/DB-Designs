Instagram Thrift Creator Store DB Design :- (ERD)

<img width="4686" height="2582" alt="Instagram Thrift Creator Store - DB design" src="https://github.com/user-attachments/assets/5961a903-8945-4160-82ea-1e9824ff237b" />

<hr/>

Eraser Code for the ERD :- 

```javascript
// Entities Required: customer, product, ThriftedProduct,
// HandmadeProduct, Order, OrderItem, Payment, Shipping 

Customer [icon: user, color: Black] {
  customer_id int pk
  name VARCHAR(50) NOT NULL
  phone_no VARCHAR(20) NOT NULL
  email VARCHAR(100)
  address text NOT NULL

  created_at timestamp
  updated_at timestamp
}

Product [icon: package] {
  product_id int pk
  name VARCHAR(100) NOT NULL
  description text 
  price INT
  product_type ENUM("THRIFTED", "HANDMADE")
  size ENUM("XS", "S", "M", "L", "XL", "XXL", "Free Size")
  color VARCHAR(20)
  image_url text
  is_available boolean

  created_at timestamp
  updated_at timestamp
}

ThriftedProduct [icon: tag, color: Orange] {
  product_id int pk fk
  condition ENUM("New", "Good", "Fair", "Worn")
  quantity int
}

HandmadeProduct [icon: scissors, color: Orange] {
  product_id int pk fk
  quantity int
  made_to_order boolean
}

Order [icon: shopping-cart, color: Green] {
  order_id integer pk
  customer_id integer fk
  order_date timestamp
  total_amount decimal
  order_status ENUM("Pending", "Confirmed", "Shipped", "Delivered", "Cancelled")
}

OrderItem [icon: list] {
  order_item_id integer pk
  order_id integer fk
  product_id integer fk
  quantity integer
  unit_price decimal
}

Payment [icon: credit-card, color: Black] {
  payment_id integer pk
  order_id integer fk
  payment_date timestamp
  amount_paid decimal
  payment_method ENUM("UPI", "Bank Transfer", "COD")
  payment_status ENUM("Pending", "Partial", "Completed")
}

Shipping [icon: truck, colorMode: pastel, color: Black] {
  shipping_id integer pk
  order_id integer fk
  recipient_name varchar
  address text
  city varchar
  pincode varchar
  shipping_status ENUM("Not Shipped", "Dispatched", "In Transit", "Delivered")
  tracking_number varchar
  shipped_date date
  delivered_date date
}

// Relationships :-
Customer.customer_id < Order.customer_id

Order.order_id < OrderItem.order_id

Product.product_id < OrderItem.product_id

Order.order_id - Payment.order_id
Order.order_id - Shipping.order_id

Product.product_id - ThriftedProduct.product_id
Product.product_id - HandmadeProduct.product_id

```


