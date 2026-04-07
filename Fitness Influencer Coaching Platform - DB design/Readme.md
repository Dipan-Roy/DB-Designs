Fitness Influencer Coaching Platform : DB - Design (ERD) :-

<img width="3932" height="2375" alt="Fitness Influencer Coaching Platform - DB design" src="https://github.com/user-attachments/assets/337dd665-e684-44eb-87be-8a48d89a747c" />

<hr/>

Eraser Code for the ERD :-

```javascript
// Entities required : client, trainer, subscription(diet_plans, workout_plans) 
// sessions(check-in), consultations, progress_tracking, , payment, feedback

Client [icon: user, color: Green] {
  client_id int pk 
  session_id int fk
  phone_no varchar not null
  email varchar not null
  address text 
  photo_url text

  created_at timestamp
  updated_at timestamp
}

Trainer [icon: dumbbell] {
  trainer_id int pk 
  client_id int fk 
  phone_no varchar not null
  photo_url text
  email varchar not null

  created_at timestamp
  updated_at timestamp
}

Subscriptions [icon: package, color: Black] {
  subscription_id int pk 
  payment_id int fk
  client_id int fk
  diet_plans boolean
  workout_plans boolean
  duration enum("monthly", "quaterly", "annually")
  price int 
}

Sessions [icon: calendar] {
  session_id int pk 
  trainer_id int fk
  subscription_id int fk
  check_in boolean
  session_duration timestamp
  session_date date
}

Consultations [icon: stethoscope] {
  consultation_id int pk
  trainer_id int fk
  client_id int fk 
  consultation_date date
  consultation_duration timestamp
  check_in_time timestamp
  check_out_time timestamp
}

Progress_tracking [icon: trending-up] {
  client_id int fk pk
  track enum("lagging", "on_track", "completed", "left")
  session_id int fk 
}

Feedback [icon: star] {
  session_id int fk pk
  trainer_id int fk
  feedback_date date
}

Payment [icon: credit-card] {
  payment_id int pk 
  client_id int fk
  subscription_id int fk
  amount int
  payment_date date
  payment_time timestamp
  is_successful boolean
  mode_of_payment enum("cash", "UPI", "card", "other")
}

// Relationships :- 
Client.client_id - Trainer.client_id
Client.client_id < Subscriptions.client_id
Client.client_id < Consultations.client_id
Client.client_id < Payment.client_id

Trainer.trainer_id < Sessions.trainer_id
Trainer.trainer_id < Consultations.trainer_id

Sessions.session_id < Client.session_id
Sessions.session_id - Feedback.session_id
Sessions.session_id - Progress_tracking.session_id

Payment.payment_id - Subscriptions.payment_id

```



