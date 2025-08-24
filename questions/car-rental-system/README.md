# Car Rental System -- Low Level Design (LLD)

## 📌 Problem Statement

Design a **Car Rental System** that allows customers to:
- Search available cars.
- Reserve a car.
- Cancel a reservation.
- Manage billing & payments.
- Track rental history.

The system should be **extensible**, **maintainable**, and designed
using **OOP principles**.

------------------------------------------------------------------------

## 🎯 High-Level Requirements

-   A user should be able to book/cancel cars.
-   Cars should be managed by stores with their own inventory.
-   Payments should support different modes (e.g., credit, wallet).
-   The system should support different vehicle types.
-   Notifications should be sent on booking/cancellation.

------------------------------------------------------------------------

## 🏗️ Class Responsibilities (Why divided like that?)

-   **User** → Represents customers with basic details (id, name,
    license).
-   **Car / Vehicle** → Abstract class for different vehicle types (SUV,
    Sedan, etc.).
-   **VehicleInventoryManagement** → Manages availability of cars in a
    store.
-   **Store** → Represents a physical location with cars &
    reservations.
-   **Reservation** → Holds booking details (user, car, dates, status).
-   **ReservationManager** → Handles lifecycle of reservations (create,
    update, cancel).
-   **Bill** → Calculates rental charges.
-   **Payment / PaymentService** → Handles different payment modes.
-   **NotificationService** → Sends booking confirmation/cancellation
    alerts.

👉 By splitting responsibilities, we:
- Avoid **God classes**.
- Keep code **modular, testable, and extensible**.
- Follow **Single Responsibility Principle (SRP)**.

------------------------------------------------------------------------

## 🧩 Design Patterns Used

-   **Factory Pattern** →
    Used for creating different vehicle objects dynamically (`SUV`,
    `Sedan`, etc.).

-   **Strategy Pattern** →
    Used in `Bill`/`Pricing` for flexible billing strategies (`HOURLY`,
    `DAILY`, `WEEKLY`).

-   **Observer Pattern** →
    `NotificationService` observes reservation events (confirmation,
    cancellation) and triggers notifications.

-   **Singleton Pattern** →
    `ReservationManager` can be singleton to avoid duplicate booking
    handling.

------------------------------------------------------------------------

## 📊 UML Class Diagram

<!-- ![Car Rental UML](./Car_Rental_System.png) -->

------------------------------------------------------------------------

## 🔄 Key Flows

### Reservation Flow

1.  User searches available cars via `VehicleInventoryManagement`.
2.  `ReservationManager` creates a new `Reservation`.
3.  `Bill` calculates charges using Strategy Pattern.
4.  `PaymentService` processes payment.
5.  `NotificationService` sends confirmation.

------------------------------------------------------------------------

## ⚡ Extensibility Points

-   Add new **vehicle types** without changing core code.
-   Add new **payment methods** easily.
-   Support **loyalty programs** or **discount strategies** by extending
    billing.

------------------------------------------------------------------------

## 📚 Learnings & Takeaways

-   Clearly defining **class responsibilities** avoids code bloat.
-   Applying **design patterns** makes the system flexible for future
    changes.
-   UML diagrams help visualize relationships & interactions.
-   Always design for **extensibility** in real-world systems.

------------------------------------------------------------------------

## 💡 Feedback

I'd love to hear how you would approach this system differently!
Feel free to suggest improvements or extend the design further 🚀

## 🔗 Go Back
[⬅️ Back to LLD Takeaways](../../README.md)
