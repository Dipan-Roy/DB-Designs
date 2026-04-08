Clinic Appointment and Diagnostics Platform - ERD 

<img width="4712" height="2855" alt="Clinic Appointment and Diagnostics Platform - DB design" src="https://github.com/user-attachments/assets/7ca15ad4-beb2-45ae-b7df-a63a4aab4a9d" />

<hr/>

Eraser code for the ERD :-

```javascript
// Clinic Appointment & Diagnostics Platform - ERD

patients [icon: user, color: blue] {
  id integer pk
  full_name string
  date_of_birth date
  gender string
  phone string
  email string
  address string
  blood_group string
  created_at timestamp
}

departments [icon: building, color: purple] {
  id integer pk
  name string
  description string
}

doctors [icon: heart, color: green] {
  id integer pk
  full_name string
  specialty string
  department_id integer fk
  phone string
  email string
  license_number string
  available_days string
}

appointments [icon: calendar, color: orange] {
  id integer pk
  patient_id integer fk
  doctor_id integer fk
  scheduled_at timestamp
  status string
  reason string
  created_at timestamp
}

consultations [icon: file-text, color: teal] {
  id integer pk
  appointment_id integer fk
  patient_id integer fk
  doctor_id integer fk
  notes string
  diagnosis string
  follow_up_date date
  consulted_at timestamp
}

diagnostic_tests [icon: activity, color: red] {
  id integer pk
  name string
  description string
  sample_type string
  normal_range string
  unit string
  cost decimal
}

prescribed_tests [icon: clipboard, color: yellow] {
  id integer pk
  consultation_id integer fk
  test_id integer fk
  status string
  prescribed_at timestamp
}

reports [icon: file, color: pink] {
  id integer pk
  prescribed_test_id integer fk
  result string
  remarks string
  is_abnormal boolean
  generated_by string
  generated_at timestamp
}

payments [icon: credit-card, color: gray] {
  id integer pk
  appointment_id integer fk
  patient_id integer fk
  amount decimal
  status string
  method string
  paid_at timestamp
}

// Relationships
departments.id < doctors.department_id
patients.id < appointments.patient_id
doctors.id < appointments.doctor_id
appointments.id - consultations.appointment_id
patients.id < consultations.patient_id
doctors.id < consultations.doctor_id
consultations.id < prescribed_tests.consultation_id
diagnostic_tests.id < prescribed_tests.test_id
prescribed_tests.id - reports.prescribed_test_id
appointments.id - payments.appointment_id
patients.id < payments.patient_id
```
