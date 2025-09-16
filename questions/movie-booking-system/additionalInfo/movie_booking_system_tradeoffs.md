# ⚖️ Trade-offs in Movie Booking System (with Scenarios)

Designing a Movie Booking System involves several trade-offs to balance **simplicity, scalability, and user experience**.  
Here are the key trade-offs I considered, with simple real-world scenarios for better understanding.

---

## 1️⃣ Seat Layout Representation

- **Matrix (2D array)** → Great for regular layouts like a multiplex with standard rows (A1–A10, B1–B10).  
  ✅ Fast lookups: `seat[A][5]`  

- **Map/List** → Useful when theatres have VIP recliners in the back or a luxury lounge with irregular arrangements.  

👉 **Example:** PVR Gold Class has sofas instead of rows — a `Map<SeatId, Seat>` works better than forcing a matrix.

---

## 2️⃣ Movie–Theatre Mapping

- **Direct Mapping** → Store which theatres run which movies directly.  
  ✅ Faster queries → *"Show me all theatres running ‘Oppenheimer’ in Hyderabad."*  
  ❌ Data redundancy → Each movie-theatre relation is repeated.  

- **Normalized Mapping** → Separate tables for Movies, Theatres, and a mapping table for shows.  
  ✅ No redundancy, scalable.  
  ❌ Slightly slower queries.  

👉 **Example:** If *Jawan* is showing in 200 theatres, direct mapping repeats the movie data in 200 places. A normalized design avoids this but needs joins.

---

## 3️⃣ Payment Flow

- **Synchronous Payment** → User selects seats → pays immediately → booking confirmed.  
  ✅ Simple to implement.  
  ❌ Risk: If payment gateway is slow, the user waits, and seats may remain blocked unnecessarily.  

- **Async + Seat Hold** → Seats are held for 5 mins → user pays → booking confirmed if payment succeeds.  
  ✅ Scales well for peak times (e.g., blockbuster releases).  
  ❌ Needs extra infra for timers and seat-release logic.  

👉 **Example:** During an Avengers premiere, 10,000 users try booking at once. Async with seat hold prevents fights over the same seat.

---

## 4️⃣ Booking Confirmation

- **Immediate Lock** → Seats are locked the moment a user clicks them.  
  ✅ Prevents double booking.  
  ❌ If the user abandons payment, seats are wasted.  

- **Temporary Hold with Expiry** → Seats are reserved for a limited time (say 5 mins). If payment fails/timeout, seats are released.  
  ✅ User-friendly, reduces wastage.  
  ❌ Needs state management & cleanup jobs.  

👉 **Example:** BookMyShow shows a countdown timer ("Your seats are held for 5:00 mins") — this is temporary hold with expiry.

---

📌 These trade-offs ensure that the system remains **robust and user-friendly**, while still being **scalable** for real-world load like movie premieres or festival releases.

[⬅️ Back To Movie Booking System ](../README.md)
