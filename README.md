Absolutely. Below is a **complete `README.md`** you can directly copy and paste into your GitHub repository.

````markdown
# 🤖 AI QA Testing Agents — n8n

An AI-powered QA automation workflow built with **n8n** that uses specialized AI agents to automate common QA engineering activities such as:

- Test Plan generation
- Test Case generation
- Bug Triage
- Root Cause Analysis (RCA)

The workflow uses **Jira as the source of requirements/bugs** and automatically stores generated QA artifacts in **Google Docs and Google Sheets**.

---

## 🚀 Project Overview

The goal of this project is to reduce repetitive QA activities by allowing a tester to provide a Jira ticket or QA request.

The workflow automatically identifies the requested QA activity and routes it to the appropriate AI Agent.

### High-Level Flow

```text
                            ┌──────────────────────┐
                            │    Chat Trigger      │
                            │   User QA Request    │
                            └──────────┬───────────┘
                                       │
                                       ▼
                            ┌──────────────────────┐
                            │   JavaScript Node    │
                            │    Parse Request     │
                            └──────────┬───────────┘
                                       │
                                       ▼
                            ┌──────────────────────┐
                            │       Switch         │
                            │   Route by Action    │
                            └───┬────┬────┬────┬───┘
                                │    │    │    │
                 ┌──────────────┘    │    │    └──────────────┐
                 │              ┌────┘    └────┐               │
                 ▼              ▼              ▼               ▼
          ┌─────────────┐┌─────────────┐┌─────────────┐┌─────────────┐
          │ Test Plan   ││ Test Case   ││ Bug Triage  ││  RCA Agent  │
          │   Agent     ││   Agent     ││   Agent     ││             │
          └──────┬──────┘└──────┬──────┘└──────┬──────┘└──────┬──────┘
                 │              │              │              │
                 ▼              ▼              ▼              ▼
          ┌─────────────┐┌─────────────┐┌─────────────┐┌─────────────┐
          │ Google Docs ││ Google      ││ Google      ││ JavaScript  │
          │   Update    ││ Sheets      ││ Sheets      ││   Parser    │
          └─────────────┘└─────────────┘└─────────────┘└──────┬──────┘
                                                                │
                                                                ▼
                                                         ┌─────────────┐
                                                         │ Google      │
                                                         │ Sheets      │
                                                         └─────────────┘               
````

---

# 🧩 AI Agents

## 1. 📝 Test Plan Agent

The Test Plan Agent creates a concise test plan from a Jira requirement or feature.

### Responsibilities

* Understand the requirement
* Define testing scope
* Identify testing approach
* Create test scenarios
* Identify risks
* Define regression impact
* Define entry/exit criteria
* Provide automation strategy
* Maintain requirement traceability

### Output

The generated test plan is stored in **Google Docs**.

### Example

```text
User:
Create a test plan for VWOAPP-2

        ↓

Jira

        ↓

Test Plan Agent

        ↓

Google Docs
```

---

# 2. 🧪 Test Case Agent

The Test Case Agent creates **exactly 3 important executable test cases** from a Jira requirement.

### Responsibilities

* Understand the requirement
* Select important scenarios
* Cover positive scenarios
* Cover negative scenarios
* Cover boundary cases when relevant
* Create executable test steps
* Define expected results

### Output

Each test case is stored as a separate row in **Google Sheets**.

### Google Sheet Columns

```text
TC ID
Title
Priority
Type
Steps
Expected Result
```

### Example

```text
User:
Create test cases for VWOAPP-2

        ↓

Jira

        ↓

Test Case Agent

        ↓

JavaScript Parser

        ↓

Google Sheets
```

---

# 3. 🐞 Bug Triage Agent

The Bug Triage Agent analyzes Jira bugs and determines their testing/engineering classification.

### Responsibilities

* Determine Severity
* Determine Priority
* Identify Bug Category
* Identify Suspected Layer
* Provide Confidence
* Recommend Action

### Severity

```text
S0
S1
S2
S3
S4
```

### Priority

```text
P0
P1
P2
P3
P4
```

### Categories

```text
Functional
UI/UX
API/Integration
Data
Performance
Security
Configuration
Other
```

### Suspected Layers

```text
Frontend
Backend
API
Database
Infrastructure
Security
Unknown
```

### Recommended Actions

```text
Hotfix Immediately
Fix in Current Sprint
Fix in Next Sprint
Investigate
Request More Information
Keep in Backlog
```

### Output

Bug triage results are stored in **Google Sheets**.

### Google Sheet Columns

```text
Jira Key
Summary
Severity
Priority
Category
Suspected Layer
Triage Rationale
Recommended Action
```

---

# 4. 🔍 RCA Agent

The RCA Agent performs Root Cause Analysis for Jira bugs/issues.

### Responsibilities

* Analyze the Jira issue
* Identify the possible root cause
* Identify affected layer
* Identify category
* Provide supporting evidence
* Recommend a fix
* Suggest prevention actions

### Output Fields

```text
Jira Key
Root Cause
Affected Layer
Category
Evidence
Fix Recommendation
Prevention
```

### Output

RCA results are stored in **Google Sheets**.

---

# 🏗️ Technology Stack

| Technology    | Purpose                           |
| ------------- | --------------------------------- |
| n8n           | Workflow automation               |
| Jira          | Requirement and bug source        |
| Groq / LLM    | AI reasoning and generation       |
| Google Docs   | Test Plan storage                 |
| Google Sheets | Test Case, Triage and RCA storage |
| JavaScript    | Data parsing and transformation   |

---

# 📋 Prerequisites

Before setting up the project, make sure you have:

* n8n instance
* Jira account/access
* Jira credentials configured in n8n
* Google account
* Google Docs access
* Google Sheets access
* LLM API key
* Imported workflow JSON

---

# ⚙️ Setup Guide

## Step 1 — Import Workflow

1. Open your n8n instance.
2. Import the workflow JSON.
3. Open the imported workflow.
4. Review all nodes.
5. Configure credentials.
6. Save the workflow.

---

# Step 2 — Configure Jira

Configure your Jira credentials in n8n.

The agents should retrieve only the information required for the requested task.

Recommended Jira fields:

```text
Issue Key
Issue Type
Summary
Description
Priority
Environment
Acceptance Criteria
Steps to Reproduce
Expected Result
Actual Result
```

### ⚠️ Important

Avoid passing unnecessary Jira data to the AI Agent such as:

```text
Changelog
Worklog
Large comment history
Attachments
Unused metadata
Large API responses
```

Keeping the Jira payload small reduces:

* Token usage
* Processing time
* Model errors
* Context size problems

---

# Step 3 — Configure LLM

Configure the Chat Model used by the AI Agents.

Example configuration:

```text
Provider: Groq
Model: Your selected supported model
API Key: Your API key
```

The selected model should support:

* Structured output
* Tool calling
* n8n AI Agent compatibility

---

# Step 4 — Configure Google Docs

The Test Plan Agent generates the test plan.

The workflow then updates an existing Google Document.

Recommended flow:

```text
Test Plan Agent
       ↓
Google Docs - Update Document
```

The Google Docs node should point to the document where the test plan needs to be stored.

---

# Step 5 — Configure Google Sheets

Create three Google Sheets or three tabs.

## Test Cases

Create columns:

```text
TC ID
Title
Priority
Type
Steps
Expected Result
```

## Bug Triage

Create columns:

```text
Jira Key
Summary
Severity
Priority
Category
Suspected Layer
Triage Rationale
Recommended Action
```

## RCA

Create columns:

```text
Jira Key
Root Cause
Affected Layer
Category
Evidence
Fix Recommendation
Prevention
```

Use:

```text
Operation: Append Row
```

for storing new results.

---

# Step 6 — JavaScript Parser

AI Agents can return JSON inside the `output` field as a string.

The JavaScript node converts this into normal n8n JSON.

## RCA Parser

Use:

```javascript
const output = $input.first().json.output;

const rca = typeof output === 'string'
  ? JSON.parse(output)
  : output;

return [
  {
    json: rca
  }
];
```

This converts:

```json
{
  "output": "{\"jira_key\":\"VWOAPP-2\",\"root_cause\":\"Unknown\"}"
}
```

into:

```json
{
  "jira_key": "VWOAPP-2",
  "root_cause": "Unknown"
}
```

---

# Step 7 — Test Case Parser

The Test Case Agent returns an array containing 3 test cases.

Use:

```javascript
const output = $input.first().json.output;

const testCases = typeof output === 'string'
  ? JSON.parse(output)
  : output;

return testCases.map(tc => ({
  json: tc
}));
```

This creates three n8n items.

```text
TC-001
   ↓
Google Sheets Row 1

TC-002
   ↓
Google Sheets Row 2

TC-003
   ↓
Google Sheets Row 3
```

---

# 🔀 Switch Node

The Switch node routes the request to the correct agent.

Recommended action values:

```text
test_plan
test_case
bug_triage
rca
```

Example:

```text
User Request
     ↓
JavaScript
     ↓
Action = test_case
     ↓
Switch
     ↓
Test Case Agent
```

### ⚠️ Important

The value must match exactly.

For example:

```text
test_case
```

is different from:

```text
Test Case
```

or:

```text
testcase
```

---

# 💬 Example Requests

## Test Plan

```text
Create a test plan for VWOAPP-2
```

Flow:

```text
Chat
 ↓
Switch
 ↓
Test Plan Agent
 ↓
Google Docs
```

---

## Test Cases

```text
Create test cases for VWOAPP-2
```

Flow:

```text
Chat
 ↓
Switch
 ↓
Test Case Agent
 ↓
JavaScript
 ↓
Google Sheets
```

---

## Bug Triage

```text
Triage bug VWOAPP-10
```

Flow:

```text
Chat
 ↓
Switch
 ↓
Bug Triage Agent
 ↓
Google Sheets
```

---

## RCA

```text
Perform RCA for VWOAPP-10
```

Flow:

```text
Chat
 ↓
Switch
 ↓
RCA Agent
 ↓
JavaScript
 ↓
Google Sheets
```

---

# 🧪 Example End-to-End Scenario

Suppose Jira contains:

```text
VWOAPP-2

Feature:
Wishlist functionality for products
```

The user sends:

```text
Create test cases for VWOAPP-2
```

The workflow performs:

```text
1. Receive Chat Request
          ↓
2. Parse Action + Jira ID
          ↓
3. Switch
          ↓
4. Retrieve Jira Details
          ↓
5. Test Case Agent
          ↓
6. Generate 3 Test Cases
          ↓
7. JavaScript Parser
          ↓
8. Google Sheets
```

Result:

```text
TC-001 → Add product to wishlist
TC-002 → Remove product from wishlist
TC-003 → Wishlist persistence / duplicate handling
```

---

# 🔐 Security

Never commit credentials or secrets to GitHub.

Do NOT commit:

```text
API Keys
Jira Tokens
Jira Passwords
Google OAuth Tokens
n8n Credentials
.env files
Private Keys
```

Use n8n Credentials or environment variables.

Recommended `.gitignore`:

```text
.env
*.env
credentials.json
*.key
*.pem
```

---

# 📁 Recommended Repository Structure

```text
ai-qa-testing-agents/
│
├── README.md
│
├── workflow/
│   └── ai-qa-testing-agents.json
│
├── prompts/
│   ├── test-plan.md
│   ├── test-case.md
│   ├── bug-triage.md
│   └── rca.md
│
└── .gitignore
```

For a simple repository:

```text
ai-qa-testing-agents/
│
├── README.md
├── ai-qa-testing-agents.json
└── .gitignore
```

---

# 🐛 Troubleshooting

## Google Sheets Error

### Error

```text
At least one value has to be added under
'Values to Send'
```

### Solution

Add the required fields under:

```text
Google Sheets
→ Values to Send
```

Example:

```text
jira_key → {{ $json.jira_key }}
root_cause → {{ $json.root_cause }}
```

---

## `rca.map is not a function`

### Cause

RCA returns a JSON object, not an array.

### Incorrect

```javascript
return rca.map(...)
```

### Correct

```javascript
return [
  {
    json: rca
  }
];
```

---

## Test Cases Not Reaching Google Sheets

Check:

1. Switch route is correct.
2. Test Case Agent executed.
3. Agent generated exactly 3 test cases.
4. JSON parser executed.
5. Parser returned 3 items.
6. Google Sheets uses `Append Row`.
7. Sheet column mappings are correct.

---

## Switch Route Not Executing

Check the output of the JavaScript node before the Switch.

Expected values:

```text
test_plan
test_case
bug_triage
rca
```

Make sure there are no:

```text
Extra spaces
Different capitalization
Different spelling
```

---

# 📊 Benefits

This workflow helps QA teams:

* Reduce repetitive manual work
* Generate test plans faster
* Generate executable test cases
* Standardize bug triage
* Perform structured RCA
* Store QA artifacts automatically
* Reduce AI token consumption
* Integrate Jira with QA workflows
* Build a foundation for AI-assisted QA engineering

---

# 🔮 Future Enhancements

Potential future agents and features:

* API Test Agent
* Playwright Automation Agent
* Selenium Automation Agent
* Regression Test Selection Agent
* Test Data Generation Agent
* API Contract Testing Agent
* Performance Testing Agent
* Security Testing Agent
* Duplicate Bug Detection Agent
* Test Execution Agent
* Test Failure Analysis Agent
* QA Dashboard
* Slack / Teams Notifications
* Jira Ticket Creation Agent

---

# 🎯 Project Goal

The long-term goal is to build an **AI QA Engineering Platform** that can automate the complete QA lifecycle.

```text
                    Jira
                     │
                     ▼
              ┌─────────────┐
              │  AI QA      │
              │  Workflow   │
              └──────┬──────┘
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
   Test Plan     Test Cases    Bug Triage
        │            │            │
        ▼            ▼            ▼
      Docs         Sheets       Sheets
                     │
                     ▼
                    RCA
                     │
                     ▼
                  Sheets
```

---

# 👨‍💻 Author

Built as an **AI-assisted QA Engineering automation project** using:

**n8n + Jira + LLM Agents + Google Docs + Google Sheets**

---

## ⭐ If you find this project useful

Feel free to ⭐ the repository and use it as a starting point for building your own AI-powered QA automation workflows.

````

### GitHub setup

Save the above as:

```text
README.md
````

Then your repository can initially contain:

```text
📁 ai-qa-testing-agents
│
├── 📄 README.md
├── 📄 ai-qa-testing-agents.json   ← exported n8n workflow
└── 📄 .gitignore
```

**Important:** Export your n8n workflow **without credentials/secrets** before uploading the JSON to GitHub.
