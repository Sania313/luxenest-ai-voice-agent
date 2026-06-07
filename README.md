# 🏠 LuxeNest AI Voice Agent

> A fully automated AI Voice Agent for home services businesses — built with Retell AI, Twilio, Cal.com, and Make.com.

---

## 🎬 Live Demo — Real Call Recording

https://youtube.com/shorts/jI0P2KzGGCU

> 👆 Click to watch a real live call — Sarah the AI agent calls a homeowner, uncovers their needs, and books a Free In-Home Estimate appointment automatically.

---

## 🎯 What This System Does

**Sarah**, the AI voice agent, automatically:
1. 📞 Calls homeowners and confirms their identity
2. 🔍 Uncovers their home service needs
3. 💬 Pitches a free in-home estimate
4. 🛡️ Handles objections professionally
5. 📅 Books a Cal.com appointment automatically
6. 🔄 Syncs all call data via Make.com webhook

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **Retell AI** | Voice agent platform — hosts Sarah the AI agent |
| **Twilio** | US phone number & SIP trunking for real calls |
| **Cal.com** | Appointment scheduling & calendar management |
| **Make.com** | Automation & webhook processing between platforms |


---

## 📞 Call Flow

```
📱 Inbound / Outbound Call
           ↓
   Stage 1: Intro & Verification
           ↓
   Stage 2: Need Uncovering
           ↓
   Stage 3: Value of Visit Pitch
           ↓
   Stage 4: Objection Handling (if needed)
           ↓
   Stage 5: Book the Appointment
           ↓
   Call Ends → Webhook → Make.com → Cal.com Booking Created ✅
```

---


## 🎭 Objection Handling

| Objection | Response Strategy |
|-----------|-----------------|
| "Not now" / Timing | Reframe estimate as a planning tool — no commitment |
| Budget Concern | Free estimate gives real numbers — zero obligation |
| Need to Talk to Spouse | Schedule when both are available |
| Lead Time Concern (6-12mo) | Plan early to beat lead times |

---

## 📋 Agent System Prompt

See [`prompts/system-prompt.txt`](prompts/system-prompt.txt) for the full Retell AI system prompt used to power Sarah.

---

## 🔧 Quick Setup

### 1. Retell AI
- Create account at [retellai.com](https://retellai.com)
- Create Voice Agent and paste system prompt
- Build 5-stage node flow on canvas
- Set webhook URL to Make.com

### 2. Twilio
- Get a US phone number
- Create Elastic SIP Trunk
- Whitelist Retell AI IP: `18.98.16.120/30`
- Connect via SIP trunking with UDP transport

### 3. Cal.com
- Create "Free In-Home Estimate" event (60 mins)
- Set availability and generate API key
- Note your Event Type ID

### 4. Make.com
- Create Custom Webhook scenario
- Add HTTP module → POST to `https://api.cal.com/v2/bookings`
- Map dynamic fields from Retell AI webhook
- Activate scenario

---

## 🔗 Webhook Data from Retell AI

```json
{
  "event": "call_analyzed",
  "call": {
    "retell_llm_dynamic_variables": {
      "customer_name": "John Smith",
      "customer_address": "123 Main St Arizona",
      "issue": "Kitchen Remodel"
    },
    "to_number": "+1xxxxxxxxxx",
    "from_number": "+14058070517",
    "transcript": "Agent: Hi this is Sarah...",
    "call_analysis": {
      "call_summary": "Agent contacted homeowner..."
    }
  }
}
```

---

## 📅 Cal.com Booking API

```json
POST https://api.cal.com/v2/bookings

{
  "eventTypeId": YOUR_EVENT_TYPE_ID,
  "start": "2026-06-09T05:00:00.000Z",
  "end": "2026-06-09T06:00:00.000Z",
  "responses": {
    "name": "{{customer_name}}",
    "email": "noemail@luxenest.com",
    "location": { "value": "inPerson", "optionValue": "" }
  },
  "timeZone": "Asia/Karachi",
  "language": "en",
  "metadata": {
    "phone": "{{customer_phone}}",
    "address": "{{customer_address}}",
    "issue": "{{issue}}"
  },
  "apiKey": "YOUR_CAL_API_KEY"
}
```

---

## 🧪 Testing Simulations

Two tests before going live:

**1. Angry Customer** — hostile caller, stop calling demand, pricing complaints

**2. Low Information Caller** — one-word answers, can't confirm address, confused about the call

---

## 📁 Project Structure

```
luxenest-ai-voice-agent/
├── README.md
├── LuxeNest_AI_Voice_Agent.docx
├── prompts/
│   └── system-prompt.txt
```

---

## 👤 Built By

**Sania** — AI Voice Agent & Automation Specialist
