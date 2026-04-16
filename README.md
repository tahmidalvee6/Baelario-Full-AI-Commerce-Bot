# 🛍️ baelario-ai-commerce-engine

> **AI-powered omnichannel commerce bot for Baelario** — an intelligent sales agent that handles jersey browsing, order taking, payment detection, and order tracking across WhatsApp, Instagram DM, Facebook Messenger, and Website Chat — all automated with n8n.

---

## 📌 Overview

**Baelario** is an online sports jersey & kit shopping platform. This repository contains the full n8n workflow engine and configuration files that power Baelario's AI commerce agent.

The agent acts as a smart, conversational sales assistant — it understands natural language, guides customers through product selection (club, jersey type, size), records orders to Google Sheets, detects payments, and provides real-time order tracking — without any human intervention.

---

## 🤖 What the AI Agent Does

### 🗣️ Natural Conversation Flow
The agent understands natural customer queries like:

```
Customer: "I want a Barcelona jersey"
Agent:    "Great choice! Do you want the Home or Away kit? 🏠✈️"
Customer: "Away please"
Agent:    "Perfect! What size? We have S, M, L, XL, XXL"
Customer: "XL"
Agent:    "Got it! 1x Barcelona Away Jersey – XL. Shall I confirm your order?"
```

### 🧠 Core Capabilities

| Feature | Description |
|---|---|
| 🔍 **Product Browsing** | Customers can ask about available jerseys, clubs, kits, and editions |
| 👕 **Jersey Selection** | Handles Home / Away / Third kit selection with size options (S, M, L, XL, XXL) |
| 📋 **Order Taking** | Collects and confirms full order details through conversation |
| 💳 **Payment Detection** | Automatically detects payment confirmations and updates order status |
| 📦 **Order Tracking** | Customers can check their order status anytime via chat |
| 📊 **Google Sheets Logging** | All orders are recorded and managed in Google Sheets in real time |

---

## 📡 Supported Platforms

| Platform | Status |
|---|---|
| 💬 WhatsApp | ✅ Active |
| 📸 Instagram DM | ✅ Active |
| 📘 Facebook Messenger | ✅ Active |
| 🌐 Website Chat | ✅ Active |

---

## 🗂️ Repository Structure

```
baelario-ai-commerce-engine/
│
├── workflows/                  # n8n workflow JSON files
│   ├── main-agent.json         # Core AI agent workflow
│   ├── order-handler.json      # Order processing workflow
│   ├── payment-detection.json  # Payment confirmation workflow
│   └── order-tracking.json     # Order status tracking workflow
│
├── config/                     # Configuration files
│   ├── products.json           # Jersey catalog (clubs, kits, sizes)
│   ├── responses.json          # AI response templates
│   └── channels.json           # Platform channel configuration
│
├── sheets/                     # Google Sheets templates
│   └── orders-template.json    # Sheets schema for order management
│
├── prompts/                    # AI system prompt files
│   └── agent-prompt.txt        # Master AI agent instructions
│
├── .env.example                # Environment variable template
├── .gitignore
└── README.md
```

---

## ⚙️ Tech Stack

| Layer | Technology |
|---|---|
| 🔄 Automation Engine | [n8n](https://n8n.io) |
| 🧠 AI Model | Claude / GPT (via n8n AI Agent node) |
| 💬 Messaging APIs | WhatsApp Business API, Meta Graph API |
| 📊 Data Storage | Google Sheets |
| 🌐 Webhook Handler | n8n Webhook Nodes |
| 🔐 Environment Config | `.env` file |

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/baelario-ai-commerce-engine.git
cd baelario-ai-commerce-engine
```

### 2. Configure Environment Variables

```bash
cp .env.example .env
```

Then open `.env` and fill in your credentials:

```env
# Messaging
WHATSAPP_API_TOKEN=your_whatsapp_token
META_APP_SECRET=your_meta_app_secret
VERIFY_TOKEN=your_webhook_verify_token

# AI
ANTHROPIC_API_KEY=your_claude_api_key
# or
OPENAI_API_KEY=your_openai_key

# Google Sheets
GOOGLE_SHEETS_ID=your_spreadsheet_id
GOOGLE_SERVICE_ACCOUNT_JSON=path/to/credentials.json

# n8n
N8N_WEBHOOK_BASE_URL=https://your-n8n-instance.com
```

### 3. Import Workflows into n8n

1. Open your **n8n instance**
2. Go to **Workflows → Import**
3. Import all `.json` files from the `/workflows/` directory
4. Activate each workflow

### 4. Set Up Google Sheets

1. Create a new Google Sheet
2. Use the schema from `/sheets/orders-template.json`
3. Share the sheet with your Google Service Account email
4. Copy the Sheet ID into your `.env`

### 5. Connect Messaging Channels

- **WhatsApp:** Register your webhook URL in Meta Business Manager
- **Instagram & Messenger:** Connect via Meta Graph API
- **Website Chat:** Embed the provided widget or connect via webhook

---

## 💬 Conversation Example

```
👤 Customer: "Do you have Real Madrid jersey?"

🤖 Baelario AI: "Yes! We have the Real Madrid 2024/25 collection 🤍
  Which kit would you like?
  1️⃣ Home (White)
  2️⃣ Away (Purple)
  3️⃣ Third (Black)"

👤 Customer: "Home please, size L"

🤖 Baelario AI: "Perfect choice! ✅
  📋 Order Summary:
  • Real Madrid Home Jersey – Size L
  • Price: ৳ 1,200
  
  Please send payment to: 01XXXXXXXXX (bKash/Nagad)
  Then reply with your payment screenshot 📸"

👤 Customer: [sends payment screenshot]

🤖 Baelario AI: "Payment confirmed! 🎉 Your order #BL-2047 is now being processed.
  Expected delivery: 2-4 business days.
  Type 'track order' anytime to check your status."
```

---

## 📋 Order Data Structure (Google Sheets)

| Column | Description |
|---|---|
| Order ID | Auto-generated unique order ID (e.g. BL-2047) |
| Customer Name | Name collected during chat |
| Phone / IG / FB ID | Platform identifier |
| Channel | WhatsApp / Instagram / Messenger / Web |
| Jersey | Club + Kit type (e.g. Barcelona Away) |
| Size | S / M / L / XL / XXL |
| Quantity | Number of items |
| Price | Total order amount |
| Payment Status | Pending / Confirmed / Failed |
| Order Status | Processing / Shipped / Delivered |
| Timestamp | Date & time of order |

---

## 🔒 Security Notes

- Never commit your `.env` file — it is listed in `.gitignore`
- Use environment variables for all API keys and tokens
- Rotate your `VERIFY_TOKEN` periodically
- Use HTTPS for all webhook endpoints

---

## 🛠️ Customization

### Adding New Jerseys / Products
Edit `/config/products.json` to add new clubs, kits, editions, or sizes.

### Changing AI Responses
Edit `/prompts/agent-prompt.txt` to adjust the agent's personality, language (e.g. Bangla/English), or conversation flow.

### Adding New Platforms
Add new webhook nodes in n8n and register them in `/config/channels.json`.

---

## 📄 License

This project is proprietary and confidential. Built exclusively for **Baelario**.  
Unauthorized distribution or reproduction is not permitted.

---

## 👤 Author

Built with ❤️ using **n8n** + **AI** for the Baelario platform.  
For support or customization inquiries, contact the development team.
