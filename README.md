# 🏥 WhatsApp AI Medical Booking Bot (n8n + Supabase + Gemini)

An end-to-end **AI-powered WhatsApp chatbot** built using **n8n**, **Google Gemini**, and **Supabase** that allows patients to:

- Book doctor appointments  
- View & manage bookings  
- Reschedule or cancel appointments  
- Chat naturally using AI  

---

## 🚀 Features

- 📱 WhatsApp webhook integration  
- 🤖 AI-powered conversation (Google Gemini)  
- 🧠 Context-aware chat with memory  
- 🗂️ Structured booking flow (name, age, symptoms, etc.)  
- 🩺 Specialty → Doctor → Slot selection  
- 🔁 Reschedule & cancel bookings  
- 💾 Persistent storage using Supabase  
- ⚡ Deduplication & rate limiting  
- 🎯 Smart intent detection  

---

## 🧩 Workflow Overview

This n8n workflow processes incoming WhatsApp messages and responds intelligently.

### 🔄 Flow Breakdown

1. **Webhook Trigger**
   - Receives incoming WhatsApp messages

2. **Message Ingestion**
   - Deduplicates messages  
   - Applies rate limiting  
   - Parses text, buttons, lists, location  

3. **Database Logging**
   - Saves user messages to Supabase  

4. **Session + History**
   - Loads session state  
   - Loads recent conversation  

5. **Context Builder**
   - Builds structured prompt for AI  
   - Tracks booking progress  

6. **AI Agent (Gemini)**
   - Generates response  
   - Calls tools (doctors, slots, bookings)

7. **Response Parser**
   - Validates AI output  
   - Handles truncation safely  

8. **Session Update**
   - Updates booking draft  
   - Tracks intent & progress  

9. **WhatsApp Formatter**
   - Converts response to:
     - Text  
     - Buttons  
     - List messages  

10. **Send Message**
   - Sends response via WhatsApp Cloud API  

---

## 🛠️ Tools (AI Functions)

The AI agent can call these tools dynamically:

- `get_specialties` → Fetch medical specialties  
- `get_doctors` → Get doctors by specialty & pincode  
- `get_slots` → Available appointment slots  
- `create_booking` → Book appointment  
- `get_bookings` → Fetch user bookings  
- `reschedule_booking` → Change slot  
- `cancel_booking` → Cancel booking  

---

## 🗄️ Database (Supabase)

Used tables/views:

- `conversation_messages` → chat history  
- `session_state` → user session & draft  
- `bookings` → appointment data  
- `v_doctor_search` → doctor listing  
- `v_available_slots` → available slots  
- `v_recent_conversation` → chat context  

---

## ⚙️ Setup Instructions

### 1. Import Workflow
- Import the provided JSON into n8n

---

### 2. Configure Credentials

#### 🔐 Supabase
- Add Supabase API credentials in n8n
- Replace:
  - `apikey`
  - `Authorization`

#### 🤖 Google Gemini
- Add Google Gemini API key  
- Connect to **AI Agent node**

#### 📱 WhatsApp Cloud API
- Set:
  - `phone_number_id`
  - `Bearer Token`

---

### 3. Webhook Setup

- Endpoint:
- - Configure in Meta Developer Dashboard  
- Verify webhook  

---

### 4. Environment Variables (Recommended)

Replace hardcoded secrets with env vars:

- `SUPABASE_URL`
- `SUPABASE_KEY`
- `WHATSAPP_TOKEN`
- `PHONE_NUMBER_ID`

---

## 🧠 AI Behavior

The AI:

- Collects patient details step-by-step  
- Maintains a **booking draft**  
- Never asks duplicate questions  
- Uses structured JSON responses  
- Calls tools when needed  

---

## 📦 Example Flow
User: Hi
Bot: What would you like to do?

User: Book appointment
Bot: What is your name?

User: Vamsi
Bot: Age?

User: 25
Bot: Symptoms?

User: Fever

→ AI selects specialty
→ Shows doctors
→ Shows slots
→ Confirms booking


---

## 🔒 Safety Features

- ✅ Deduplication (prevents duplicate messages)  
- ✅ Rate limiting (1 msg / 1.5 sec)  
- ✅ JSON validation for AI responses  
- ✅ Fallback response handling  
- ✅ Secure booking (phone + booking_ref match)  

---

## ⚠️ Important Notes

- Never expose API keys publicly  
- Move secrets to environment variables  
- Ensure Supabase RLS policies are configured  
- WhatsApp API requires approved templates for outbound messages  

---

## 📌 Future Improvements

- 💳 Payment integration  
- 🌍 Multi-language support  
- 🧑‍⚕️ Doctor availability sync  
- 📊 Admin dashboard  
- 📅 Calendar integrations  

---

## 🙌 Credits

Built using:

- n8n  
- Supabase  
- Google Gemini  
- WhatsApp Cloud API  
