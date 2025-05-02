# Team Roles
## Backend Developer
Responsible for building and maintaining the server-side logic, APIs, and core application functionality. Ensures smooth communication between the database, server, and frontend.

## Frontend Developer
Creates the user interface and experience (UI/UX) using web technologies. Ensures responsiveness, accessibility, and performance on the client side.

## Database Administrator (DBA)
Designs and manages the project's database systems. Responsible for data modeling, optimization, backups, and ensuring data integrity and security.

## QA Engineer / Tester
Develops and executes test plans to ensure the software is bug-free and meets requirements. Conducts manual and automated testing, and reports issues for fixing.

## Project Manager
Oversees the entire project life cycle. Coordinates the team, manages timelines and deliverables, communicates with stakeholders, and ensures project goals are met.

## DevOps Engineer
Automates deployment, monitors infrastructure, and manages CI/CD pipelines. Ensures scalability, performance, and system reliability throughout the development cycle.


# Technology Stack
## Django
A high-level Python web framework used to build robust, scalable, and secure web applications. It handles the server-side logic, routing, and RESTful API development.

## PostgreSQL
An open-source relational database management system (RDBMS) used to store and manage application data. Known for its performance, reliability, and advanced querying features.

## GraphQL
A query language for APIs that allows clients to request exactly the data they need. Used to improve efficiency and flexibility in data fetching between the frontend and backend.

## Docker
A containerization tool that packages the application and its dependencies into isolated environments, making deployment and scaling more consistent and efficient.

# Database Design
The Airbnb Clone Project is structured around a relational database schema designed to reflect real-world interactions on a booking platform. Below is a high-level overview of the core entities, their attributes, and how they interconnect to form a functional, scalable system.

## Users
Represents both hosts and guests using the platform.

Field	Type	Description
id	Integer	Primary key
full_name	String	User's full name
email	String	Unique email address
password_hash	String	Encrypted password
role	Enum	Either "host", "guest", or both

### Relationships:

One user can own multiple properties.

One user can create multiple bookings.

One user can write multiple reviews.

One user can make multiple payments.

## Properties
Represents listings created by hosts.

Field	Type	Description
id	Integer	Primary key
owner_id	Integer	Foreign key → Users.id
title	String	Property listing title
description	Text	Detailed property description
price_per_night	Decimal	Nightly rate
address	String	Physical address of the property

### Relationships:

One property is owned by one user.

One property can have many bookings and reviews.

## Bookings
Manages reservation data between guests and properties.

Field	Type	Description
id	Integer	Primary key
user_id	Integer	Foreign key → Users.id (guest)
property_id	Integer	Foreign key → Properties.id
start_date	Date	Start date of the booking
end_date	Date	End date of the booking
status	Enum	Status (e.g., pending, confirmed)

### Relationships:

One booking is made by one user for one property.

One booking may have one payment.

## Reviews
Captures feedback from guests about properties.

Field	Type	Description
id	Integer	Primary key
user_id	Integer	Foreign key → Users.id
property_id	Integer	Foreign key → Properties.id
rating	Integer	Rating (1 to 5)
comment	Text	Optional review content

### Relationships:

A review is written by one user for one property.

## Payments
Logs financial transactions related to bookings.

Field	Type	Description
id	Integer	Primary key
booking_id	Integer	Foreign key → Bookings.id
amount	Decimal	Payment amount
method	String	Payment method (e.g., card, PayPal)
status	Enum	(e.g., completed, failed, refunded)

### Relationships:

One payment is associated with one booking.

### Entity Relationship Summary
User ⟶ (1:N) ⟶ Properties

User ⟶ (1:N) ⟶ Bookings

User ⟶ (1:N) ⟶ Reviews

Property ⟶ (1:N) ⟶ Bookings

Property ⟶ (1:N) ⟶ Reviews

Booking ⟶ (1:1) ⟶ Payment