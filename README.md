# 🎫 Customer Support Ticket Analyzer using Gemini API

An AI-powered **Customer Support Ticket Analyzer** built with **Python and Google Gemini API**. The application analyzes customer support messages and automatically identifies the issue category, customer sentiment, priority level, generates a professional response, and suggests the next action for the support team.

The project demonstrates how **Generative AI and structured JSON output** can be integrated into a real-world customer-support workflow.

---

## 📌 Project Overview

Customer support teams receive a large number of messages through email and chat. Manually reading and categorizing every ticket can be time-consuming.

This project uses **Gemini Flash** to automatically analyze customer messages and return structured information that can be used by a support system.

### Input

A customer support message such as:

> "I was charged twice for the same order. I have already emailed support twice and nobody has responded. I need this fixed immediately."

### Output

```json
{
  "category": "Billing",
  "sentiment": "Frustrated",
  "priority": "High",
  "response": "We apologize for the duplicate charge and the delay in responding. Our team will review the transaction and assist you with the refund.",
  "next_action": "Verify the duplicate transaction and initiate a refund if confirmed."
}
```

---

## ✨ Features

* 🤖 AI-powered customer support ticket analysis
* 🏷️ Automatic issue categorization
* 😊 Sentiment detection
* 🚨 Priority assignment: Low, Medium, or High
* 💬 Automatic professional customer response generation
* 🛠️ Recommended next action for support teams
* 📦 Structured JSON output
* 🔄 Reusable Python function for processing multiple tickets
* 🧠 Gemini thinking-level configuration
* 📋 Response schema for consistent structured output

---

## 🧠 What the AI Analyzes

For every customer message, the system generates:

| Field         | Description                             |
| ------------- | --------------------------------------- |
| `category`    | Type of customer issue                  |
| `sentiment`   | Customer's emotional tone               |
| `priority`    | Low, Medium, or High                    |
| `response`    | Professional response to the customer   |
| `next_action` | Recommended action for the support team |

---

## 🏗️ Workflow

```text
Customer Message
       ↓
Python Application
       ↓
Gemini API
       ↓
System Instruction
       ↓
Gemini Analysis
       ↓
Response Schema
       ↓
Structured JSON
       ↓
Category + Sentiment + Priority
       ↓
Customer Response + Next Action
```

---

## 🛠️ Technologies Used

* **Python**
* **Google Gemini API**
* **Google GenAI Python SDK**
* **JSON**
* **Google Colab / Jupyter Notebook**

---

## 📚 Gemini API Concepts Demonstrated

### 1. Gemini API Integration

The project uses the Google GenAI Python SDK to communicate with the Gemini model.

```python
from google import genai

client = genai.Client(api_key=api_key)
```

### 2. `generate_content()`

Used to send the customer message to Gemini and generate the analysis.

```python
response = client.models.generate_content(
    model="gemini-3.5-flash",
    contents=customer_message
)
```

### 3. System Instruction

The model is given a specific role as a professional customer support ticket analyzer.

```text
You are a professional customer support ticket analyzer.
```

### 4. Structured JSON Output

The response is configured to return JSON rather than unstructured text.

```python
response_mime_type="application/json"
```

### 5. Response Schema

A schema defines the expected structure of the JSON response.

```text
category
sentiment
priority
response
next_action
```

### 6. Thinking Level

The project demonstrates controlling the model's reasoning effort through the thinking configuration.

### 7. Max Output Tokens

The maximum generated output length is controlled using:

```python
max_output_tokens=300
```

### 8. Reusable Function

The ticket analysis logic is wrapped inside a reusable function:

```python
def analyze_ticket(customer_message):
    ...
```

This allows multiple support tickets to be processed efficiently.

---

## 📂 Project Structure

```text
Customer-Support-Ticket-Analyzer/
│
├── Customer_Support_Ticket_Analyzer.ipynb
├── README.md
└── requirements.txt
```

---

## ⚙️ Installation

Clone the repository:

```bash
git clone https://github.com/your-username/Customer-Support-Ticket-Analyzer.git
```

Move into the project directory:

```bash
cd Customer-Support-Ticket-Analyzer
```

Install the required package:

```bash
pip install -q google-genai
```

---

## 🔑 API Key Configuration

The project requires a Gemini API key.

For Google Colab, store the API key in **Colab Secrets** using:

```text
GEMINI_API_KEY
```

Then access it using:

```python
from google.colab import userdata

api_key = userdata.get("GEMINI_API_KEY")
```

Create the Gemini client:

```python
from google import genai

client = genai.Client(api_key=api_key)
```

> ⚠️ Never upload your API key directly to GitHub or expose it in public code.

---

## 🧪 Example Tickets

The project can analyze different types of customer-support issues, including:

### 💳 Billing Issue

```text
I was charged twice for my subscription this month.
I have checked my bank statement and both transactions
were completed. Please refund the duplicate charge.
```

### 🖥️ Technical Issue

```text
The application crashes every time I try to upload a PDF.
I have restarted my computer and reinstalled the application,
but the problem is still happening.
```

### 🔐 Account / Password Issue

```text
I forgot my password and requested a password reset three
times, but I still haven't received the reset email.
I need access to my account urgently.
```

### 📦 Delivery Issue

```text
My order was supposed to arrive three days ago, but the
tracking information hasn't changed since it left the warehouse.
Can you please tell me where my package is?
```

### 🎓 General / Low Priority

```text
I would like to know whether you offer a student discount
and what documents are required to qualify for it.
```

---

## 📊 Example Output

```json
{
  "category": "Billing",
  "sentiment": "Frustrated",
  "priority": "High",
  "response": "We apologize for the duplicate charge and the delay in responding. Our team will review the transaction and assist you with the refund.",
  "next_action": "Verify the duplicate transaction and initiate a refund if confirmed."
}
```

---

## 🎯 Key Learning Outcomes

Through this project, I learned how to:

* Integrate the Gemini API with Python
* Work with the Google GenAI Python SDK
* Securely manage API keys
* Create reusable Gemini API functions
* Design effective system instructions
* Use structured JSON responses
* Define response schemas
* Configure model thinking levels
* Control output length using token limits
* Process multiple customer-support tickets
* Convert AI-generated JSON into Python dictionaries
* Apply Generative AI to a real-world business use case

---

## 🚀 Future Improvements

Possible improvements include:

* Add a web interface using **Streamlit**
* Store analyzed tickets in a database
* Add ticket ID and customer information
* Create a support-team dashboard
* Add automatic email response functionality
* Add multilingual ticket analysis
* Add confidence scores
* Connect the system with a CRM/helpdesk platform
* Add batch processing for CSV files
* Deploy the application as an API using FastAPI

---

## 👨‍💻 Author

**Aman**

This project was created as part of my learning journey in **Data Science, Generative AI, and Gemini API integration**.

---

## ⭐ If you find this project useful

Consider giving the repository a ⭐ on GitHub.
