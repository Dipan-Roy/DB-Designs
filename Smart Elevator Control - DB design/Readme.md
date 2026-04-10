Smart Elevator Control ERD :-

<img width="6404" height="2538" alt="Smart Elevator Control - DB design" src="https://github.com/user-attachments/assets/11f563b2-5a03-4f33-b76f-052edf5d26bf" />

<hr/>

Eraser code for the ERD :-

```javascript
// Smart Elevator Control - ERD

Building [icon: building, color: blue] {
  building_id int pk
  name varchar(50)
  building_type enum("residental", "commercial", "mall", "corporate")
  total_floors int 
  total_elevators int
}

Floor [icon: layers, color: teal] {
  floor_id int pk
  building_id int fk
  floor_no int
  floor_type enum("basement", "ground", "terrace", "normal")
  floor_name varchar(20)
}

Elevator [icon: arrow-up, color: gray] {
  elevator_id int pk
  building_id int fk
  floor_id int fk
  max_capacity int 
  max_weight_kg int
  max_floor int
  min_floor int
  installed_at date
}

Elevator_status [icon: activity, color: purple] {
  elevator_id int fk pk
  status enum("idle", "maintenance", "going up", "going down", "disabled")
  current_floor_id int fk
  last_updated timestamp
}

Floor_requests [icon: bell, color: red] {
  floor_request_id int pk
  building_id int fk
  floor_id int fk
  req_status enum("ongoing", "upcoming", "completed", "failed")
  req_at timestamp
  duration timestamp
}

Ride_assignment [icon: link, color: orange] {
  assignment_id int pk
  floor_request_id int fk
  elevator_id int fk
  assigned_at timestamp
  assignment_status enum(ASSIGNED, IN_PROGRESS, COMPLETED, FAILED)
}

Ride_log [icon: file-text, color: green] {
  id int pk
  assignment_id int fk
  elevator_id int fk
  origin_floor_id int fk
  destination_floor_id int fk
  trip_start timestamp
  trip_end timestamp
  duration_seconds int
  passenger_load_estimate int
}

Maintenance_record [icon: tool, color: pink] {
  id int pk
  elevator_id int fk
  maintenance_type enum(ROUTINE, EMERGENCY, INSPECTION, UPGRADE)
  scheduled_at timestamp
  started_at timestamp
  completed_at timestamp
  technician_name varchar(100)
  technician_contact varchar(15)
  remarks varchar(500)
  maintenance_status enum(SCHEDULED, IN_PROGRESS, COMPLETED, CANCELLED)
}

// Relationships :-
Building.building_id < Floor.building_id
Building.building_id < Elevator.building_id

Floor.floor_id < Elevator.floor_id

Elevator.elevator_id < Floor_requests.floor_request_id

Floor_requests.floor_request_id - Floor.floor_id

Ride_assignment.floor_request_id - Floor_requests.floor_request_id
Ride_assignment.elevator_id - Elevator.elevator_id

Elevator_status.elevator_id - Elevator.elevator_id
Elevator_status.current_floor_id - Floor.floor_id

Maintenance_record.elevator_id - Elevator.elevator_id

Ride_log.assignment_id - Ride_assignment.assignment_id
Ride_log.elevator_id - Elevator.elevator_id
Ride_log.origin_floor_id - Floor.floor_id
Ride_log.destination_floor_id - Floor.floor_id

```
