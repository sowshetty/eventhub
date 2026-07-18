# Functional Requirements Document (FRD)

---

## Document Information

| Field | Value |
|-------|--------|
| Project | EventHub |
| Document | Functional Requirements Document (FRD) |
| Version | 1.0 |
| Status | Draft |
| Author | Naveen Krishna |
| Last Updated | 19 July 2026 |

---

# 1. Purpose

The purpose of this document is to define the functional requirements of the EventHub application.

This document describes how the system should behave from the user's perspective. It specifies the features, business rules, validations, and expected behavior without describing technical implementation details.

The Functional Requirements Document serves as a bridge between business requirements and software design.

---

# 2. Functional Overview

EventHub is an enterprise-grade cloud-native Event Management System that enables users to discover events, organizers to manage events, and administrators to monitor the platform.

The application provides secure authentication, event management, booking management, search functionality, and administrative capabilities.

---

# 3. User Roles

The system supports three user roles.

## 3.1 Customer

A customer can:

- Register
- Login
- View profile
- Search events
- View event details
- Book tickets
- View booking history
- Cancel bookings before the event starts

---

## 3.2 Organizer

An organizer can:

- Login
- Create events
- Update events
- Delete events
- Publish events
- Cancel events
- View bookings for their events

---

## 3.3 Administrator

An administrator can:

- Manage users
- Manage organizers
- Manage events
- Block users
- Activate users
- View platform reports
- Monitor system activity

---

# 4. Functional Requirements

---

## FR-001 User Registration

Description

The system shall allow new users to register.

Inputs

- Full Name
- Email Address
- Password
- Mobile Number (Optional)

Expected Behaviour

- Validate user input.
- Check duplicate email.
- Encrypt password.
- Save user details.
- Return successful registration response.

---

## FR-002 User Login

Description

The system shall authenticate registered users.

Expected Behaviour

- Validate credentials.
- Generate JWT Token.
- Return access token.
- Reject invalid credentials.

---

## FR-003 View User Profile

The user shall be able to view their profile information after successful authentication.

---

## FR-004 Update Profile

Authenticated users shall be able to update profile information except email.

---

## FR-005 Create Event

Organizer shall be able to create a new event.

Required Information

- Event Title
- Description
- Venue
- Event Date
- Event Time
- Maximum Capacity
- Category

Expected Behaviour

- Validate inputs.
- Store event.
- Mark event as Draft initially.

---

## FR-006 Publish Event

Organizer shall be able to publish an event.

Published events become visible to customers.

---

## FR-007 Update Event

Organizer shall be able to modify event details before the event starts.

---

## FR-008 Delete Event

Organizer shall be able to delete unpublished events.

---

## FR-009 Search Events

Users shall be able to search events using

- Event Name
- Location
- Category
- Date

The search results shall support pagination.

---

## FR-010 View Event Details

Users shall be able to view

- Event information
- Organizer
- Date
- Time
- Available seats
- Category
- Venue

---

## FR-011 Book Event

Authenticated users shall be able to book tickets.

Expected Behaviour

- Verify authentication.
- Verify seat availability.
- Create booking.
- Reduce available seats.
- Generate Booking ID.

---

## FR-012 View Bookings

Users shall be able to view all previous bookings.

---

## FR-013 Cancel Booking

Users shall be able to cancel bookings before the event starts.

Cancelled seats become available again.

---

## FR-014 Admin User Management

Administrator shall be able to

- View users
- Block users
- Activate users
- Delete users (future enhancement)

---

## FR-015 Admin Event Management

Administrator shall be able to

- View all events
- Remove inappropriate events
- Disable events

---

# 5. Business Rules

## User Management

- Email must be unique.
- Password must be encrypted.
- JWT Token required for secured APIs.

---

## Event

- Event date cannot be in the past.
- Capacity must be greater than zero.
- Event title cannot be empty.
- Organizer owns the event.

---

## Booking

- Booking allowed only if seats are available.
- Duplicate booking for the same event by the same user is not allowed.
- Booking cannot exceed available capacity.
- Cancel booking only before event start time.

---

# 6. Validation Rules

## Registration

Mandatory

- Name
- Email
- Password

Optional

- Mobile Number

---

## Login

Mandatory

- Email
- Password

---

## Event Creation

Mandatory

- Title
- Description
- Venue
- Date
- Capacity
- Category

---

## Booking

Mandatory

- Event ID

---

# 7. Error Handling

The system shall return meaningful error messages.

Examples

| Scenario | Message |
|-----------|----------|
| Duplicate Email | Email already registered |
| Invalid Login | Invalid email or password |
| Unauthorized | Authentication required |
| Forbidden | Access denied |
| Event Not Found | Event does not exist |
| Event Full | No seats available |
| Invalid Date | Event date cannot be in the past |
| Booking Exists | Booking already exists |

---

# 8. Functional Flow

Customer Flow

Register

↓

Login

↓

Search Events

↓

View Event

↓

Book Ticket

↓

View Booking History

---

Organizer Flow

Login

↓

Create Event

↓

Publish Event

↓

Manage Event

↓

View Bookings

---

Administrator Flow

Login

↓

Manage Users

↓

Manage Events

↓

Generate Reports

---

# 9. Assumptions

- Users have internet connectivity.
- JWT Authentication will be used.
- Email verification will be added in a future release.
- Payment gateway is outside Version 1.0.
- Notification service will be implemented in a later phase.

---

# 10. Out of Scope

The following features are excluded from Version 1.0.

- Online Payments
- Refund Management
- QR Code Entry Validation
- Mobile Application
- AI Event Recommendation
- Social Login
- Live Chat
- Multi-language Support

---

# 11. Future Enhancements

- Payment Gateway
- Email Notifications
- SMS Notifications
- QR Code Tickets
- AI Event Recommendations
- Event Analytics Dashboard
- Mobile Application
- Calendar Integration
- Social Login

---

# 12. Version History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | 19 July 2026 | Naveen Krishna | Initial Functional Requirements Document |

---