# Airbnb Clone Backend

## Objective

Identify and document the backend features and functionalities required for the Airbnb Clone project. Provide a clear, actionable reference for developers and learners.

## Overview

This document lists core backend features, endpoints, data models, and implementation notes. Use it as the README for the features-and-functionalities directory.

## Contents

* Core features and descriptions
* API endpoint examples and expected behavior
* Data model summary (tables and key fields)
* Diagram reference (features-and-functionalities-diagram.png)
* How to export a Draw\.io diagram to PNG
* Git commit and push instructions

---

## Core Features

1. User Management

* Register as guest or host
* Login with email and password
* OAuth login (Google, Facebook)
* Profile update and photo upload
* Role based access: guest, host, admin

2. Property Listings

* Create listing with title, description, location, price, amenities, availability, images
* Edit and delete listing by host
* Listing visibility and status (active, inactive)

3. Search and Filtering

* Search by location, price range, guest capacity, amenities
* Pagination and sorting
* Geospatial support for radius search

4. Booking Management

* Create booking with date range and guest count
* Prevent double booking with date conflict checks
* Booking lifecycle: pending, confirmed, canceled, completed
* Cancellation rules and refunds

5. Payments

* Integrate Stripe or PayPal for payments
* Charge guest at booking time or at check-in depending on policy
* Payouts to hosts after completion or on scheduled intervals
* Multi-currency support and currency conversion notes

6. Reviews and Ratings

* Post-review only after completed stay
* Ratings aggregated per property and per host
* Host response to reviews

7. Notifications

* Email and in-app notifications for booking events, payments, messages, admin alerts
* Use SendGrid or Mailgun for emails

8. Admin Dashboard

* Manage users, listings, bookings, payments
* Audit logs and activity monitoring
* Fraud detection flags and manual interventions

9. Media Storage

* Store images in cloud storage or local storage for development
* Use signed URLs for secure access

10. Logging and Monitoring

* Structured logs for APIs
* Error tracking with tools like Sentry

---

## Example API Endpoints

User

* POST /api/auth/register
* POST /api/auth/login
* GET /api/users/\:id
* PATCH /api/users/\:id

Listings

* POST /api/listings
* GET /api/listings
* GET /api/listings/\:id
* PATCH /api/listings/\:id
* DELETE /api/listings/\:id

Bookings

* POST /api/bookings
* GET /api/bookings/\:id
* PATCH /api/bookings/\:id (status updates)
* GET /api/users/\:id/bookings

Payments

* POST /api/payments/checkout
* POST /api/payments/webhook

Reviews

* POST /api/reviews
* GET /api/listings/\:id/reviews

Notifications

* GET /api/notifications
* POST /api/notifications/send

---

## Data Model Summary

Users

* id, name, email, password\_hash, role, profile\_photo\_url, created\_at, updated\_at

Properties

* id, host\_id, title, description, address, latitude, longitude, price\_per\_night, currency, amenities, status, created\_at, updated\_at

Bookings

* id, property\_id, guest\_id, host\_id, start\_date, end\_date, total\_amount, currency, status, created\_at, updated\_at

Payments

* id, booking\_id, amount, currency, provider, provider\_payment\_id, status, created\_at

Reviews

* id, booking\_id, property\_id, reviewer\_id, rating, comment, created\_at

Notifications

* id, user\_id, type, payload, is\_read, created\_at

---

## Diagram

A visual diagram is provided as features-and-functionalities-diagram.png. It maps the main backend components and their relationships.

If you prefer to create or edit the diagram in Draw\.io, follow these steps:

1. Open draw\.io or diagrams.net.
2. Create a new blank diagram.
3. Use rectangular shapes to represent components: Users, Auth, Listings, Bookings, Payments, Reviews, Notifications, Admin, Storage, Search.
4. Connect components with arrows showing data flow and ownership: Users to Listings, Users to Bookings, Bookings to Payments, Bookings to Reviews.
5. Export using File > Export as > PNG. Choose 2x scale for higher resolution. Save the file as features-and-functionalities-diagram.png.

---

## File structure suggested in repo

features-and-functionalities/

* README.md
* features-and-functionalities-diagram.png
* spec.md (optional detailed specs)

---

## Git commands to add the diagram and README to your repository

Run the following in your project root:

mkdir -p features-and-functionalities

# copy README.md into features-and-functionalities/ and place diagram PNG there

git add features-and-functionalities/README.md features-and-functionalities/features-and-functionalities-diagram.png
git commit -m "Add features and functionalities doc and diagram for Airbnb Clone backend"
git push origin main

Adjust the branch name if your default branch name differs from main.

---

## Next steps for learners

1. Use the README as the source of truth when implementing backend APIs.
2. Convert core features into user stories and tasks in your project board.
3. Create ER diagram from the data model summary and update the diagram as the schema evolves.
4. Implement tests for booking validation and payment flows.
