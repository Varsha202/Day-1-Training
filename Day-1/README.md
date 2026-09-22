# 🤖 AI Day 1 Lab

## Agentic AI: Foundations and Open-Source Practice

This lab demonstrates three different approaches to solving the same college course-fee problem:

1. **Plain LLM Chatbot**
2. **Rule-Based Workflow**
3. **Tool-Using AI Agent**

The main goal is to understand the difference between a traditional chatbot, a deterministic workflow, and an AI agent that can dynamically select and use tools.

---

## 🎯 1. Objective

The objectives of this lab are:

* Set up a Python environment for AI application development.
* Connect an application to an LLM using Groq.
* Build a plain LLM chatbot.
* Build a rule-based workflow.
* Build a tool-using AI agent.
* Compare all three approaches using the same questions.
* Observe the agent's tool-calling process.
* Test the systems with a new challenge question.

---

## 🛠️ 2. Technologies Used

| Technology           | Purpose                         |
| -------------------- | ------------------------------- |
| Python 3.13.5        | Programming language            |
| OpenAI Python SDK    | LLM integration                 |
| Groq API             | LLM provider                    |
| `openai/gpt-oss-20b` | Language model                  |
| `python-dotenv`      | Environment variable management |
| Git                  | Version control                 |
| GitHub               | Code hosting                    |

---

## 📁 3. Project Structure

```text
AI-Day-1-Lab/
│
├── .gitignore
├── requirements.txt
├── config.py
├── check_setup.py
├── chatbot.py
├── workflow.py
├── tools.py
├── agent.py
└── challenge.py
```

### Environment File

The `.env` file contains the Groq API key and is intentionally excluded from GitHub using `.gitignore`.

```text
.env
```

---

# 💰 4. Course Fee Data

The private course-fee data used in this lab is:

| Course |     Fee |
| ------ | ------: |
| CS101  | ₹12,000 |
| AI202  | ₹18,000 |
| DS303  | ₹15,000 |

---

# ❓ 5. Questions Used

### Q1

> What is the fee for AI202?

### Q2

> What is the total fee for CS101 and AI202 after a 10% scholarship?

### Q3

> Is DS303 more expensive than CS101, and by how much?

### Q4

> Write a two-line welcome message for new AI students.

---

# 💬 6. System 1 — Plain LLM Chatbot

The chatbot sends the question directly to the LLM without providing the private course-fee data or any tools.

## Output

### Q1

**Question:**

> What is the fee for AI202?

**Answer:**

> I'm happy to help! Could you let me know which college or university you're referring to? The fee for a course labeled "AI202" can vary depending on the institution, program level, and whether it's a credit or non-credit course.

### Q2

**Question:**

> What is the total fee for CS101 and AI202 after a 10% scholarship?

**Answer:**

> Sure! To calculate the total fee after a 10% scholarship, I'll need the original tuition amounts for each course.

### Q3

**Question:**

> Is DS303 more expensive than CS101, and by how much?

**Answer:**

> I'm not sure of the current prices for those courses. Could you let me know how much DS303 and CS101 cost?

### Q4

**Question:**

> Write a two-line welcome message for new AI students.

**Answer:**

> Welcome to the AI Academy!
> Embark on a journey where curiosity fuels innovation and every challenge becomes an opportunity.

### Observation

The chatbot can generate general natural-language responses, but it does not have access to the private course-fee information.

---

# ⚙️ 7. System 2 — Rule-Based Workflow

The workflow uses predefined rules and does **not** use an LLM.

## Output

```text
=== SYSTEM 2: RULE-BASED WORKFLOW (no LLM) ===

Q: What is the fee for AI202?
A: Fee for AI202: Rs. 18,000

Q: What is the total fee for CS101 and AI202 after a 10% scholarship?
A: Total fee: Rs. 27,000

Q: Is DS303 more expensive than CS101, and by how much?
A: Sorry, I do not have a rule for this type of question.

Q: Write a two-line welcome message for new AI students.
A: Sorry, I can only answer questions about course fees.
```

### Observation

The rule-based workflow is reliable for questions covered by its predefined rules, but it cannot handle questions outside those rules.

---

# 🤖 8. System 3 — Tool-Using AI Agent

The AI agent combines an LLM with external tools.

The agent uses two tools:

### `get_course_fee`

Retrieves the fee of a specific course.

### `calculator`

Performs arithmetic calculations.

The agent can:

1. Understand the user's question.
2. Decide which tools are required.
3. Execute the required tools.
4. Observe the tool results.
5. Perform additional actions if required.
6. Generate the final response.

---

## Agent Output

### Q1

**Question:**

> What is the fee for AI202?

```text
Step 1:
get_course_fee({'course_code': 'AI202'})
→ 18000
```

**Answer:**

> The fee for AI202 is ₹18,000.

---

### Q2

**Question:**

> What is the total fee for CS101 and AI202 after a 10% scholarship?

```text
Step 1:
get_course_fee({'course_code': 'CS101'})
→ 12000

Step 2:
get_course_fee({'course_code': 'AI202'})
→ 18000

Step 3:
calculator({'expression': '(12000+18000)*0.9'})
→ 27000.0
```

**Answer:**

> The total fee for CS101 and AI202 after a 10% scholarship is ₹27,000.

---

### Q3

**Question:**

> Is DS303 more expensive than CS101, and by how much?

```text
Step 1:
get_course_fee({'course_code': 'DS303'})
→ 15000

Step 2:
get_course_fee({'course_code': 'CS101'})
→ 12000

Step 3:
calculator({'expression': '15000-12000'})
→ 3000
```

**Answer:**

> Yes. DS303 costs ₹15,000, while CS101 costs ₹12,000.
>
> Difference: DS303 is ₹3,000 more expensive than CS101.

---

### Q4

**Question:**

> Write a two-line welcome message for new AI students.

**Answer:**

> Welcome to the AI program!
> We're thrilled to have you join our community of innovators and thinkers.

---

# 🧪 9. Challenge Question

## Question

> I can pay Rs. 30,000. Which two courses can I take together within this budget?

---

## Rule-Based Workflow Output

```text
--- WORKFLOW ---

Sorry, I can only answer questions about course fees.
```

The workflow cannot handle this question because no predefined rule exists for this type of task.

---

## Agent Output

The agent dynamically checks the course fees and calculates possible combinations.

```text
Step 1:
get_course_fee({'course_code': 'CS101'})
→ 12000

Step 2:
get_course_fee({'course_code': 'AI202'})
→ 18000

Step 3:
get_course_fee({'course_code': 'DS303'})
→ 15000

Step 4:
calculator({'expression': '12000+18000'})
→ 30000

Step 5:
calculator({'expression': '12000+15000'})
→ 27000
```

### Valid Combinations

| Courses       | Total Fee |
| ------------- | --------: |
| CS101 + AI202 |   ₹30,000 |
| CS101 + DS303 |   ₹27,000 |

Both combinations are within the ₹30,000 budget.

---

# 📊 10. Observations

The following table is based on the actual runs performed during the lab.

| Criterion                        | Chatbot                   | Workflow               | Agent                         |
| -------------------------------- | ------------------------- | ---------------------- | ----------------------------- |
| Q1 correct?                      | ❌ No                      | ✅ Yes                  | ✅ Yes                         |
| Q2 correct?                      | ❌ No                      | ✅ Yes                  | ✅ Yes                         |
| Q3 correct?                      | ❌ No                      | ❌ No                   | ✅ Yes                         |
| Q4 handled well?                 | ✅ Yes                     | ❌ No                   | ✅ Yes                         |
| Challenge question handled?      | Not tested                | ❌ No                   | ✅ Yes                         |
| Same output on repeat run?       | Not tested                | Not tested             | Not tested                    |
| Approximate response time        | ~3.84 s                   | ~0.99 s                | ~7.2 s                        |
| Number of LLM calls per question | 1                         | 0                      | Varies                        |
| Main strength                    | Simple and conversational | Fast and predictable   | Flexible and tool-using       |
| Main weakness                    | No access to private data | Rigid predefined rules | Depends on LLM/tool-calling   |
| Best suited for                  | General conversation      | Fixed rule-based tasks | Dynamic tasks requiring tools |

---

# 🔍 11. Agent Trace — Question 2

## Question

> What is the total fee for CS101 and AI202 after a 10% scholarship?

| Step | Tool Called                       | Result |
| ---: | --------------------------------- | -----: |
|    1 | `get_course_fee('CS101')`         |  12000 |
|    2 | `get_course_fee('AI202')`         |  18000 |
|    3 | `calculator('(12000+18000)*0.9')` |  27000 |

### Final Result

```text
₹27,000
```

This demonstrates how an agent can combine multiple tool calls to solve a problem.

---

# ⏱️ 12. Response Time Measurements

The response times were measured using PowerShell `Measure-Command`.

## Chatbot

```text
TotalSeconds : 3.8363288
```

Approximate response time:

```text
~3.84 seconds
```

## Workflow

```text
TotalSeconds : 0.9887608
```

Approximate response time:

```text
~0.99 seconds
```

## Agent

First measurement:

```text
TotalSeconds : 7.4108674
```

Second measurement:

```text
TotalSeconds : 6.9904537
```

Approximate response time:

```text
~7.2 seconds
```

---

# 🔎 13. Key Comparison

## 💬 Chatbot

* Uses only the LLM.
* Does not have access to private course-fee data.
* Can generate natural-language responses.
* Cannot reliably answer questions requiring unavailable private information.

## ⚙️ Workflow

* Uses predefined rules.
* Does not require an LLM.
* Fast and predictable.
* Fails when a question is outside the predefined rules.

## 🤖 Agent

* Uses an LLM together with tools.
* Can select appropriate tools.
* Can combine multiple tool results.
* Can perform calculations using the calculator tool.
* Can handle new questions more flexibly.
* Tool-calling behavior depends on the LLM.

---

# 🧰 14. Setup

## Step 1 — Clone the Repository

```bash
git clone https://github.com/GOWSHIKA21/day1_lab.git
cd day1_lab
```

---

## Step 2 — Create a Virtual Environment

```bash
python -m venv venv
```

---

## Step 3 — Activate the Virtual Environment

### Windows PowerShell

```powershell
venv\Scripts\Activate.ps1
```

### Windows CMD

```cmd
venv\Scripts\activate
```

### macOS / Linux

```bash
source venv/bin/activate
```

---

## Step 4 — Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Required Packages

```text
openai>=1.40.0
python-dotenv>=1.0.0
```

---

# 🔐 15. Environment Variables

Create a `.env` file in the project root.

```env
PROVIDER=groq
GROQ_API_KEY=YOUR_GROQ_API_KEY
MODEL=openai/gpt-oss-20b
```

Replace:

```text
YOUR_GROQ_API_KEY
```

with your actual Groq API key.

### ⚠️ Security Warning

Never commit or share the `.env` file because it contains your API key.

Add the following to `.gitignore`:

```gitignore
.env
venv/
__pycache__/
*.pyc
```

---

# ▶️ 16. How to Run

## Check Setup

```bash
python check_setup.py
```

## Run Chatbot

```bash
python chatbot.py
```

## Run Rule-Based Workflow

```bash
python workflow.py
```

## Run Tools

```bash
python tools.py
```

## Run AI Agent

```bash
python agent.py
```

## Run Challenge

```bash
python challenge.py
```

---

# 🧠 17. Understanding the Three Approaches

The experiment can be summarized as follows:

```text
                 USER QUESTION
                       │
                       ▼
        ┌──────────────────────────┐
        │                          │
        │      Three Systems       │
        │                          │
        └──────────────────────────┘
             │       │       │
             ▼       ▼       ▼
          CHATBOT WORKFLOW  AGENT
             │       │       │
             ▼       ▼       ▼
            LLM     RULES   LLM + TOOLS
             │       │       │
             │       │       ├── get_course_fee
             │       │       │
             │       │       └── calculator
             │       │
             ▼       ▼       ▼
           ANSWER  ANSWER   ANSWER
```

### Plain LLM Chatbot

```text
Question
   ↓
LLM
   ↓
Answer
```

### Rule-Based Workflow

```text
Question
   ↓
Predefined Rules
   ↓
Answer
```

### Tool-Using Agent

```text
Question
   ↓
LLM
   ↓
Select Tool
   ↓
Execute Tool
   ↓
Observe Result
   ↓
Select Next Tool
   ↓
Final Answer
```

---

# 📈 18. Why the Agent Is Different

The major difference is **tool usage and dynamic decision-making**.

A normal chatbot receives a question and generates a response.

A rule-based workflow follows predefined instructions.

An agent can decide:

* Which information it needs.
* Which tool to use.
* How many tools are required.
* Whether another tool call is necessary.
* How to combine the results.

For example:

```text
User:
"I can pay ₹30,000. Which two courses can I take?"

                ↓

Agent understands the task

                ↓

Get CS101 fee
Get AI202 fee
Get DS303 fee

                ↓

Calculate combinations

                ↓

Compare against ₹30,000

                ↓

Return valid combinations
```

This allows the agent to handle a question that was not explicitly defined as a predefined workflow rule.

---

# 📝 19. Final Result

The experiment demonstrated the differences between:

* A plain LLM chatbot
* A rule-based workflow
* A tool-using AI agent

The **chatbot** was able to generate natural-language responses but did not have access to private course-fee data.

The **workflow** was fast and predictable for predefined cases but was rigid when presented with new question types.

The **agent** used tools to retrieve course information and perform calculations, allowing it to handle the challenge question by combining multiple tool results.

---

# 🎯 20. Key Takeaways

### Chatbot

> Good for general conversation and natural-language generation.

### Workflow

> Good for predictable tasks with clearly defined rules.

### Agent

> Useful when a system needs to dynamically use tools and combine information to solve a task.

---

# 👩‍💻 Author

**AI Day 1 Lab — Agentic AI Foundations and Open-Source Practice**

---

## ⭐ Conclusion

This lab provides a practical introduction to **Agentic AI** by comparing three progressively capable approaches:

```text
Plain LLM
   ↓
Rule-Based Workflow
   ↓
Tool-Using AI Agent
```

The experiment shows how adding tools and tool-selection capabilities allows an AI system to move beyond simple text generation toward more dynamic task solving.
