businessrequirements.md is a Markdown document that describes what the business expects the system to do.

For your Odysseus cruise booking system, this file should explain the requirements in business terms, not the detailed implementation.

.md means Markdown

For example:

businessrequirements.md

is simply a text file written using Markdown syntax.

You can open it in VS Code, GitHub, etc.

What should be inside your businessrequirements.md?

For this assignment, I would structure it like this:

# Business Requirements – Cruise Booking System


## 1. Purpose


The system will allow customers to search for cruises,
select travellers, choose extras, calculate the total price,
apply promotional codes, and confirm bookings.


The business must be able to permanently determine:
- What was sold
- Who purchased it
- Who travelled
- What extras were included
- What promotional discount was applied
- How much was charged

Then define the actual requirements.

1. Cruise Search
The customer should be able to:
- Search available cruises
- Select a destination
- Select a departure date
- View cruise duration
- View available cabin options
- View applicable prices
2. Travellers
The customer should be able to provide traveller information.


A booking may contain multiple travellers.


The system must distinguish between:
- The customer making the booking
- The travellers included in the booking
3. Extras
Customers should be able to select optional extras such as:
- Excursions
- Wi-Fi
- Transfers
- Dining packages


The system must include selected extras in the booking price.
4. Pricing
The system must calculate the total booking price based on:
- Cruise price
- Traveller/cabin selection
- Selected extras
- Applicable discounts


The final price must be calculated by the system and
must not be trusted from the client/frontend.
5. Promotional Codes
Customers should be able to enter a promotional code.


The system must validate:
- Whether the code exists
- Whether it is currently valid
- Whether the booking meets its conditions
- Whether any usage restrictions apply


The applicable discount must be reflected in the final price.
6. Booking Confirmation
The customer should be able to review the complete booking
before confirmation.


After confirmation, the system should generate a unique
booking reference.
7. Historical Record

This is probably the most important requirement.

Once a booking is confirmed, the system must permanently
retain the exact commercial details of the transaction.


This must include:
- Customer
- Travellers
- Cruise
- Departure
- Cabin
- Extras
- Quantity of each item
- Price of each item at booking time
- Promotional code
- Discount
- Final amount
- Currency
- Booking date/time

The booking's historical prices must not change when the current cruise or extra prices change.

Business requirement vs technical design

This distinction is important for your assignment.

businessrequirements.md

Answers:

What does the business need?

Example:

Customers must be able to apply promotional codes.
architecture.md

Answers:

How will we build it?

Example:

The backend will expose POST /promotions/validate
and the pricing service will calculate the discount.
database.md

Answers:

How will we store it?

Example:

booking_items will store the unit_price used
at the time of booking.

So for your Odysseus assignment, I would probably create separate files such as:

project/
│
├── businessrequirements.md
├── architecture.md
├── database-design.md
├── api-design.md
├── README.md
│
├── backend/
│   ├── main.py
│   ├── models/
│   ├── services/
│   ├── routes/
│   └── ...
│
└── frontend/
    └── ...

businessrequirements.md should come first, because it establishes what you're trying to solve. Then your architecture and database design can demonstrate how you decided to solve it.
