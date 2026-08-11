# Gemini AI Projects --- Resume Screening & Customer Support Ticket Analyzer

A collection of two practical Generative AI projects built with
**Python** and the **Google Gemini API**. These notebooks demonstrate
how Gemini can be used for structured business automation through system
instructions, JSON response schemas, and reusable Python functions.

## 📌 Projects Included

### 1. AI Resume Screening Assistant

The Resume Screening Assistant automates the initial screening of
candidates against a job description.

It accepts: - A **Job Description** - A **Candidate Resume**

It analyzes the candidate and returns: - **Fit classification** ---
Strong Fit, Partial Fit, or Not a Fit - **Key skills** - **Years of
experience** - **Reason for the decision** - **Shortlist
recommendation**

The output is generated as structured JSON.

### 2. Customer Support Ticket Analyzer

The Customer Support Ticket Analyzer analyzes customer messages received
through email or chat and converts them into actionable support
information.

It identifies: - **Category** - **Sentiment** - **Priority** -
**Professional customer response** - **Next action for the support
team**

The analyzer also supports processing multiple customer tickets using a
reusable function.

------------------------------------------------------------------------

## 🎯 Objective

The main objective of this project collection is to demonstrate how
Generative AI can be integrated into practical business workflows using
the Gemini API.

The projects focus on:

-   Prompt/system-instruction based AI processing
-   Structured JSON generation
-   Schema-constrained responses
-   Reusable Python functions
-   Automated decision support
-   Customer communication generation
-   Candidate screening automation

------------------------------------------------------------------------

## 🏗️ Overall Architecture

``` text
                    ┌─────────────────────┐
                    │      User Input     │
                    └──────────┬──────────┘
                               │
               ┌───────────────┴────────────────┐
               │                                │
               ▼                                ▼
     ┌───────────────────┐          ┌──────────────────────┐
     │ Job Description +  │          │ Customer Support     │
     │ Resume             │          │ Message              │
     └─────────┬─────────┘          └──────────┬───────────┘
               │                               │
               └───────────────┬───────────────┘
                               ▼
                    ┌─────────────────────┐
                    │     Python +        │
                    │     Gemini API      │
                    └──────────┬──────────┘
                               ▼
                    ┌─────────────────────┐
                    │ System Instruction  │
                    └──────────┬──────────┘
                               ▼
                    ┌─────────────────────┐
                    │ Gemini Model        │
                    │ Analysis            │
                    └──────────┬──────────┘
                               ▼
                    ┌─────────────────────┐
                    │ Response Schema     │
                    │ JSON Output         │
                    └──────────┬──────────┘
                               ▼
                    ┌─────────────────────┐
                    │ Structured Business │
                    │ Result              │
                    └─────────────────────┘
```

------------------------------------------------------------------------

# 🔹 Project 1: AI Resume Screening Assistant

## Problem Statement

Companies may receive hundreds of resumes for different job openings.
Manually reviewing every resume against a job description can be
time-consuming.

This project demonstrates an AI-assisted initial screening workflow that
compares the candidate's resume with the job requirements and provides a
structured recommendation.

## Input

The model receives:

``` text
Job Description
+
Candidate Resume
```

Example job requirements used in the notebook include:

-   Python
-   Machine Learning
-   SQL
-   3+ years of experience
-   NLP experience preferred

## Output

The response follows this structure:

``` json
{
  "fit": "Strong Fit",
  "skills": [
    "Python",
    "Machine Learning",
    "SQL",
    "NLP",
    "AWS",
    "Docker"
  ],
  "experience_years": 4,
  "reason": "Candidate meets the core requirements and has preferred NLP experience.",
  "shortlist": true
}
```

The notebook demonstrates a sample candidate who is classified as a
**Strong Fit** and recommended for shortlisting.

## Key Implementation

The project uses the Google GenAI Python SDK:

``` python
from google import genai
from google.genai import types
from google.colab import userdata
import json
```

The Gemini client is initialized using a Colab secret:

``` python
api_key = userdata.get("GEMINI_API_KEY")
client = genai.Client(api_key=api_key)
```

A reusable function handles resume analysis:

``` python
def analyze_resume(job_description_input, resume_input):
    response = client.models.generate_content(
        model="gemini-3.6-flash",
        contents=[job_description_input, resume_input],
        config=types.GenerateContentConfig(
            system_instruction=system_instruction,
            response_mime_type="application/json",
            response_schema=response_schema,
            thinking_config=types.ThinkingConfig(
                thinking_level="low"
            ),
            max_output_tokens=500
        )
    )

    return response.text
```

------------------------------------------------------------------------

# 🔹 Project 2: Customer Support Ticket Analyzer

## Problem Statement

Companies receive customer-support requests through channels such as
email and chat. Support teams need to understand the issue, determine
urgency, respond professionally, and decide what action should be taken.

This project automates that initial analysis using Gemini.

## Input

``` text
Customer Support Message
```

Example:

``` text
I was charged twice for the same order.

I have already emailed support twice and nobody
has responded. I need this fixed immediately.
```

## Output

The model generates:

``` json
{
  "category": "Billing and Payments",
  "sentiment": "Negative",
  "priority": "High",
  "response": "Professional customer response...",
  "next_action": "Investigate the duplicate transaction and initiate a refund."
}
```

## Supported Analysis

The system identifies:

  Field         Purpose
  ------------- ------------------------------------------------
  Category      Identifies the type of customer issue
  Sentiment     Determines the customer's emotional tone
  Priority      Estimates urgency
  Response      Generates a professional customer-facing reply
  Next Action   Recommends the next support-team action

## Example Ticket Categories Demonstrated

The notebook tests multiple types of support messages, including:

-   Billing and refunds
-   Technical support
-   Account access
-   Shipping and delivery
-   Pricing and discounts

## Multiple Ticket Processing

The project includes a reusable function:

``` python
def analyze_ticket(customer_message):
    response = client.models.generate_content(
        model="gemini-3.5-flash",
        contents=customer_message,
        config=types.GenerateContentConfig(
            system_instruction=system_instruction,
            response_mime_type="application/json",
            response_schema=response_schema,
            thinking_config=types.ThinkingConfig(
                thinking_level="low"
            ),
            max_output_tokens=300
        )
    )

    return response.text
```

Multiple customer messages can then be analyzed using a loop:

``` python
for i, message in enumerate(messages, start=1):
    result = analyze_ticket(message)
    print(result)
```

The notebook also converts the JSON response into a Python dictionary
for easier access:

``` python
data = json.loads(result)

print(data["category"])
print(data["sentiment"])
print(data["priority"])
print(data["response"])
print(data["next_action"])
```

------------------------------------------------------------------------

# 🧠 Core Gemini Concepts Demonstrated

## 1. Gemini API Integration

Both projects use the Google GenAI Python SDK to communicate with a
Gemini model.

``` python
from google import genai
from google.genai import types
```

## 2. API Key Management

The notebooks retrieve the API key from Google Colab Secrets:

``` python
api_key = userdata.get("GEMINI_API_KEY")
```

**Do not hard-code API keys in source code or commit them to GitHub.**

## 3. System Instructions

System instructions define the role and expected behavior of the model.

For example, the support-ticket analyzer instructs Gemini to analyze:

1.  Category
2.  Sentiment
3.  Priority
4.  Professional response
5.  Next action

## 4. Structured Output

Both projects use:

``` python
response_mime_type="application/json"
```

This makes the expected response machine-readable.

## 5. Response Schema

A JSON schema defines the expected fields and data types.

This helps make the generated output consistent and easier to process
programmatically.

## 6. Reusable Functions

The notebooks convert the Gemini API calls into reusable functions:

``` text
analyze_resume()
analyze_ticket()
```

This makes the implementations easier to reuse for additional inputs.

------------------------------------------------------------------------

# 🛠️ Tech Stack

  Technology             Usage
  ---------------------- ---------------------------------------
  Python                 Core programming language
  Google Gemini API      Generative AI processing
  Google GenAI SDK       Gemini API integration
  Google Colab           Development and execution environment
  JSON                   Structured AI output
  Python `json` module   Parsing structured responses

------------------------------------------------------------------------

# 📁 Suggested Repository Structure

``` text
gemini-ai-projects/
│
├── README.md
│
├── notebooks/
│   ├── AI Resume Screening Assistant with Gemini.ipynb
│   └── Customer-Support-Ticket-Analyzer-using-Gemini-API.ipynb
│
└── screenshots/
    └── ...
```

------------------------------------------------------------------------

# ⚙️ Installation & Setup

## 1. Clone the Repository

``` bash
git clone <your-repository-url>
cd gemini-ai-projects
```

## 2. Install the Gemini SDK

``` bash
pip install -q google-genai
```

## 3. Configure Gemini API Key

In Google Colab:

**Secrets → Add new secret**

Use:

``` text
Name: GEMINI_API_KEY
Value: YOUR_GEMINI_API_KEY
```

The notebooks retrieve it using:

``` python
from google.colab import userdata

api_key = userdata.get("GEMINI_API_KEY")
```

## 4. Open the Notebooks

Open either notebook in Google Colab or a compatible Jupyter environment
and run the cells sequentially.

------------------------------------------------------------------------

# 🔐 Security

Never commit your Gemini API key to GitHub.

Avoid:

``` python
api_key = "YOUR_REAL_API_KEY"
```

Prefer a secret/environment-based approach such as:

``` python
api_key = userdata.get("GEMINI_API_KEY")
```

Also consider adding sensitive local configuration files to
`.gitignore`.

------------------------------------------------------------------------

# ⚠️ Model Configuration Note

The two source notebooks currently reference different model identifiers
in their API calls:

-   Resume Screening Assistant: `gemini-3.6-flash`
-   Customer Support Ticket Analyzer: `gemini-3.5-flash`

The Resume Screening notebook's introductory text describes it as using
**Gemini 3.5 Flash**, while its actual API call uses `gemini-3.6-flash`.

Before running the notebooks, verify that the model identifiers are
valid and available for your Gemini API account, and standardize them if
you want both projects to use the same model.

------------------------------------------------------------------------

# 📊 Example Use Cases

## Resume Screening

Potential applications include:

-   Initial candidate screening
-   Resume-to-job-description matching
-   Skill extraction
-   Experience extraction
-   Recruiter shortlist assistance

## Customer Support

Potential applications include:

-   Automatic ticket categorization
-   Sentiment analysis
-   Priority detection
-   Drafting customer responses
-   Support-team action recommendations
-   Batch ticket analysis

------------------------------------------------------------------------

# 🚀 Future Improvements

The current notebooks demonstrate the core Gemini API workflow. A
production-ready implementation could be extended with:

### Resume Screening

-   PDF/DOCX resume upload
-   Batch resume processing
-   Job-description database
-   Candidate ranking
-   Skill-gap analysis
-   Recruiter dashboard
-   ATS integration
-   Persistent candidate records

### Customer Support

-   Email and chat integration
-   Ticket database
-   Automatic ticket routing
-   SLA-based priority rules
-   Support-agent dashboard
-   Conversation history
-   Human approval before sending responses
-   Analytics for recurring support issues

------------------------------------------------------------------------

# 📚 Learning Outcomes

By working through these projects, you can understand how to:

-   Integrate Gemini with Python
-   Securely load API credentials
-   Design system instructions
-   Pass structured inputs to an LLM
-   Define response schemas
-   Generate structured JSON responses
-   Parse JSON responses in Python
-   Build reusable Gemini API functions
-   Process multiple inputs
-   Apply Generative AI to real-world business workflows

------------------------------------------------------------------------

# 👨‍💻 Author

**Aman**

Data Science & AI Learner \| Python \| Machine Learning \| Generative AI

------------------------------------------------------------------------

## ⭐ Project Highlights

``` text
✓ Gemini API Integration
✓ Python-based AI Applications
✓ Prompt / System Instruction Design
✓ Structured JSON Output
✓ Response Schema
✓ Reusable Functions
✓ Resume Screening Automation
✓ Customer Support Automation
✓ Multiple Ticket Analysis
✓ Practical Business Use Cases
```

If you find this project useful, consider giving the repository a ⭐ on
GitHub.
