# 🏥 WhatsApp Healthcare Automation

This is a WhatsApp-based healthcare booking system built using n8n, Supabase, and AI.

The goal is simple. A patient can message on WhatsApp, describe their problem, and book a doctor for home visit without confusion.

---

## 🚀 What this system does

- Patient sends message on WhatsApp  
- AI chats and collects details step by step  
- System creates a booking request  
- Nearby doctors get notified  
- First doctor who accepts gets the booking  
- Patient gets confirmation on WhatsApp  

Just like Uber but for doctors.

---

## ⚙️ Features

- WhatsApp chatbot flow  
- Smart symptom understanding  
- Auto doctor specialty detection  
- Step by step booking flow  
- Booking confirmation and tracking  
- Cancel booking option  
- Session memory using database  
- Rate limit and duplicate handling  

---

## 🧠 AI Behaviour

- Talks in simple and friendly way  
- Does not repeat questions  
- Supports buttons and text replies  
- Detects emergency cases  
- Allows booking for family members  

---

## 🗂️ Workflow Overview

1. **Webhook**  
   Receives WhatsApp messages  

2. **Ingest Message**  
   Extracts user message, buttons, location  

3. **Database (Supabase)**  
   - Stores messages  
   - Stores session state  
   - Stores bookings  

4. **AI Agent**  
   - Understands input  
   - Decides next step  
   - Generates response  

5. **Tools**
   - get_specialties  
   - create_booking_request  
   - get_bookings  
   - cancel_booking  

6. **Response Formatter**  
   Converts AI output into WhatsApp format  

7. **Send WhatsApp**  
   Sends response back to user  

---

## 📦 Tech Stack

- n8n  
- Supabase  
- WhatsApp Cloud API  
- Gemini AI  

---

## 📌 Booking Flow

1. Symptoms  
2. Pincode  
3. Date  
4. Time slot  
5. Patient name  
6. Age  
7. Gender  
8. Summary  
9. Confirmation  

---

## 💡 Example

User: `Fever and headache`  
Bot: Asks details  
User: Gives info  
Bot: Books doctor  

---

## 🔒 Notes

- User does not select doctor  
- System assigns doctor automatically  
- Works only in supported areas  
- Emergency cases redirected to helpline  

---

## 🙌 Goal

Make doctor home visits simple and fast using WhatsApp.
