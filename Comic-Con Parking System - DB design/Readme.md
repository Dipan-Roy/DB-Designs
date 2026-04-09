Comic-Con Parking System ERD :-

<img width="6458" height="3133" alt="Comic-Con Parking System - DB design" src="https://github.com/user-attachments/assets/0f28cc93-a86c-4850-be74-5544805afd35" />

<hr/>

Eraser code for the ERD :-

```javascript
// Comic-Con India - Parking Management System ERD

vehicle_category [icon: tag, color: purple] {
  id INT pk
  name ENUM ("BIKE", "CAR", "SUV", "CAB", "EV")
  
}

access_category [icon: shield, color: orange] {
  id INT pk
  name ENUM (GENERAL, COSPLAYER, EXHIBITOR, VIP, STAFF)
  description VARCHAR(255)
}

vehicle [icon: truck, color: blue] {
  id INT pk
  license_plate VARCHAR(20)
  owner_name VARCHAR(100)
  contact_number VARCHAR(15)
  vehicle_category_id INT fk
  access_category_id INT fk
}

parking_zone [icon: map, color: green] {
  id INT pk
  zone_code VARCHAR(10)
  zone_name VARCHAR(100)
  description VARCHAR(255)
}

parking_level [icon: layers, color: teal] {
  id INT pk
  level_number INT
  level_label VARCHAR(20)
  zone_id INT fk
  total_spots INT
}

spot_category [icon: star, color: yellow] {
  id INT pk
  name ENUM (GENERAL, COSPLAYER, EXHIBITOR, VIP, STAFF, EV_CHARGING)
  is_reserved BOOLEAN
}

parking_spot [icon: parking, color: cyan] {
  id INT pk
  spot_number VARCHAR(20)
  status ENUM (AVAILABLE, OCCUPIED, RESERVED, MAINTENANCE)
  level_id INT fk
  spot_category_id INT fk
  compatible_vehicle_category_id INT fk
}

parking_session [icon: clock, color: red] {
  id INT pk
  vehicle_id INT fk
  spot_id INT fk
  access_category_id INT fk
  entry_time TIMESTAMP
  exit_time TIMESTAMP
  duration_minutes INT
  status ENUM (ACTIVE, COMPLETED, CANCELLED)
}

parking_ticket [icon: file-text, color: pink] {
  id INT pk
  ticket_number VARCHAR(30)
  issued_at TIMESTAMP
  session_id INT fk
  barcode VARCHAR(100)
}

payment [icon: credit-card, color: gray] {
  id INT pk
  session_id INT fk
  amount DECIMAL(10,2)
  payment_method ENUM (CASH, CARD, UPI, WALLET)
  payment_status ENUM (PENDING, COMPLETED, FAILED, REFUNDED)
  paid_at TIMESTAMP
  transaction_ref VARCHAR(100)
}

// Relationships
vehicle_category.id < vehicle.vehicle_category_id
access_category.id < vehicle.access_category_id

parking_zone.id < parking_level.zone_id

parking_level.id < parking_spot.level_id
spot_category.id < parking_spot.spot_category_id
vehicle_category.id < parking_spot.compatible_vehicle_category_id

vehicle.id < parking_session.vehicle_id
parking_spot.id < parking_session.spot_id
access_category.id < parking_session.access_category_id

parking_session.id - parking_ticket.session_id
parking_session.id < payment.session_id
```
