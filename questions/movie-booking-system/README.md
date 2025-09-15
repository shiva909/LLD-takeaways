# 🎬 Movie Booking System – Low-Level Design (LLD)

This project explores the **Low-Level Design (LLD)** of a Movie Booking System (similar to BookMyShow).  
The focus is on **class responsibilities, trade-offs, and extensibility** while keeping the design modular and OOP-driven.

---

## 📌 Problem Statement

Design a **Movie Booking System** where users can:

- Browse movies or theatres in a selected city.
- Select shows and seats.
- Book tickets and complete payment.

The system should support **two booking flows**:
1. **Browse by Movie** → Movie → Theatre → Show → Seat → Payment  
2. **Browse by Theatre** → Theatre → Movie → Show → Seat → Payment  
<!-- The design should support **two different booking flows**:  
1️⃣ **Browse by Movies** → Movie → Theatre → Show → Seat → Payment  
2️⃣ **Browse by Cinemas (Theatres)** → Theatre → Movie → Show → Seat → Payment   -->

The system should be modular, extensible, and scalable.

---

## 🎯 High-Level Requirements

- Support multiple cities, theatres, screens, shows, and movies.
- Flexible seat layouts and categories (Silver, Gold, Platinum).
- Seat availability checks to prevent double bookings.
- Support multiple payment methods (Card, UPI, Cash).
- Unified facade for end-to-end booking flow.
- Support both **movie-first** and **theatre-first** booking flows.

---

## 🏗️ Class Responsibilities

- **City** → Represents a city and groups theatres.
- **Theatre** → Holds screens and is tied to a city.
- **Screen** → Manages seats and shows.
- **Seat** → Defines seat id, category, row, and price.
- **Show** → Maps a movie to a screen with timings and booked seats.
- **Movie** → Stores basic details like id and name.
- **Booking** → Tracks user, show, seats, theatre, and payment.
- **User** → Represents the customer making the booking.
- **Payment** → Encapsulates payment details.

👉 By splitting responsibilities, we:
- Keep the system modular and maintainable.
- Ensure separation of concerns.
- Support both **movie-first** and **theatre-first** booking flows.

---

## 🧩 Design Patterns Considered

- **Factory Pattern** → For seat creation (`SeatFactory`).
- **Strategy Pattern** → For flexible payment methods (UPI, Card, Cash, etc.).
- **Singleton** → For globally unique managers/services.
- **Facade Pattern** → `MovieBookingFacade` simplifies client interaction with multiple services.

---

## 📊 UML Class Diagram

<img width="1749" height="1409" alt="bms_liked_0" src="https://github.com/user-attachments/assets/f5dbc907-faaf-4f1c-80f9-b51af17cc529" />

---

## 🔄 Key Flows

### 🔹 Flow A: Browse by Movies (Recommended)

1. User selects a **City**.
2. User browses **Movies** in that city.
3. Selects a **Movie** → system shows all **Theatres + Screens + Shows** for that movie.
4. Picks **Theatre + Show**.
5. Proceeds to **Seat Selection → Payment → Booking Confirmation**.

### 🔹 Flow B: Browse by Theatres

1. User selects a **City**.
2. User browses **Theatres** in that city.
3. Selects a **Theatre** → system shows all **Movies + Shows** running there.
4. Picks **Movie + Show**.
5. Proceeds to **Seat Selection → Payment → Booking Confirmation**.

---

## ⚖️ Trade-offs Considered

### 1. Seat Layout Representation
- **Matrix** → Fast lookups, intuitive layout.
- **List/Map** → Flexible for luxury/irregular seat layouts.

### 2. Movie–Theatre Mapping
- **Direct mapping** → Faster queries for one flow, but duplicates data.
- **Normalized mapping** → Avoids redundancy but adds query overhead.

### 3. Payment Flow
- **Synchronous Payment** → Simple, but may block booking.
- **Async Payment + Seat Hold** → Scalable, needs extra infrastructure.

### 4. Booking Confirmation
- **Immediate lock** → Prevents double booking, may waste seats.
- **Temporary hold with expiry** → User-friendly, requires state management.

---

## ⚡ Extensibility Points

- Add support for discounts, coupons, loyalty programs.
- Introduce seat recommendations (best available).
- Add notifications (SMS/Email) after booking.
- Support multi-currency payments for global rollout.
- Extend to online streaming/OTT integration.

---

## 📚 Learnings & Takeaways

- Modeling entities (`City → Theatre → Screen → Show → Seat`) provides clarity.
- Supporting multiple flows ensures flexibility and user-centric design.
- Separation of services (Booking, Payment, Theatre, Movie) improves maintainability.
- Design patterns (Strategy, Factory, Facade) simplify complexity and extensibility.
- Trade-offs like Matrix vs Map for seats, Synchronous vs Async payment are critical for scaling.

---

## 💡 Feedback

I’d love to hear how you would extend this **Movie Booking System** to handle **millions of concurrent bookings** 🚀

## 🔗 Go Back
[⬅️ Back to LLD Takeaways](../../README.md)
