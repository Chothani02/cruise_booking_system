technical-approach.md is a document that explains how you plan to technically solve the business requirements.

In your Odysseus cruise booking assignment:

businessrequirements.md → What does the business need?
technical-approach.md → How will we build it?
database-design.md → How will we store the data?
README.md → How does someone run/use the project?
Simple example

Business requirement:

Customer should be able to apply a promotional code.

Technical approach:

The backend will provide a promotion validation API. The pricing service will validate the code, check its validity period and booking conditions, calculate the discount, and return the updated price breakdown.

What I would put in your technical-approach.md

For this assignment, something like:

# Technical Approach


## 1. Architecture


The system will use a modular monolithic architecture.


Frontend
    ↓
FastAPI Backend
    ↓
Business Logic
    ↓
PostgreSQL Database


The backend will be divided into modules for:
- Cruise search
- Traveller management
- Pricing
- Promotions
- Booking
2. Technology Stack
Frontend:
React


Backend:
Python + FastAPI


Database:
PostgreSQL


ORM:
SQLAlchemy


Validation:
Pydantic


Testing:
Pytest


Containerization:
Docker
3. Cruise Search

Explain how the system finds cruises.

Customer provides:
- Destination
- Departure date
- Number of travellers


Backend queries available cruise departures
and returns matching cruises and available options.
4. Pricing

Explain the pricing flow:

Cruise price
      +
Cabin price
      +
Traveller pricing
      +
Extras
      -
Promotion
      ↓
Final price

The backend recalculates the price rather than trusting a price sent by the frontend.

5. Booking

Explain what happens when the customer confirms:

Validate availability
       ↓
Recalculate price
       ↓
Validate promotion
       ↓
Create booking
       ↓
Create booking items
       ↓
Store traveller information
       ↓
Reserve inventory
       ↓
Confirm booking

These operations should happen inside a database transaction.

6. Historical Pricing

This is the most important technical decision.

When a booking is confirmed, store the actual prices used:

booking_items


item_name
quantity
unit_price
total_price

Don't calculate old booking totals using today's cruise catalogue price.

For example:

2026 booking:
Cruise = ₹100,000


2027 current cruise price:
Cruise = ₹150,000

The 2026 booking must still show:

₹100,000

Therefore, confirmed booking data acts as a historical snapshot.

7. Concurrency

Explain how you prevent two customers from booking the same cabin.

For example:

Customer A ──┐
             ├── Check availability
Customer B ──┘

The database transaction should lock/reserve the relevant inventory so that both customers cannot successfully purchase the same limited cabin.

8. Idempotency

This is another good point to mention.

Suppose the customer clicks:

Confirm Booking
Confirm Booking

twice because the network is slow.

You don't want:

Booking #1001
Booking #1002

for the same transaction.

Use an idempotency key for the confirmation request so repeated requests produce the same result.

9. API Design

You can describe APIs such as:

GET  /cruises
GET  /cruises/{id}
GET  /cruises/{id}/availability


POST /quotes
POST /promotions/validate


POST /bookings
GET  /bookings/{id}
POST /bookings/{id}/confirm
POST /bookings/{id}/cancel
10. Error Handling

Examples:

Cruise unavailable
Invalid promotion
Expired promotion
Cabin no longer available
Invalid traveller details
Price changed
Payment failure
Duplicate booking request

The API should return appropriate HTTP status codes and useful error messages.

The difference you should remember

Think of your files like this:

File	Main question
businessrequirements.md	What should the system do?
technical-approach.md	How will we build it?
database-design.md	How will we store the information?
api-design.md	How will frontend/backend communicate?
README.md	How do I run and understand the project?

For the Odysseus assignment, technical-approach.md is where you demonstrate your engineering thinking—architecture, pricing logic, transactions, concurrency, historical data, APIs, security, and error handling.
