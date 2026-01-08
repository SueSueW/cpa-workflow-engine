# One-Page Operational Workflow  
_From Practice Questions to Workflow App_

This document defines the **end-to-end operational process** for extracting, validating, and publishing decision rules used by the CPA Workflow Engine.

The workflow prioritizes **human judgment first**, with AI used strictly for structured extraction and formatting.

---

## 0. One-Time Setup (Asset Preparation)

Complete once before starting:

- ✅ Save all required prompts:
  - Question solving
  - Per-question trigger & pitfall extraction
  - Two-step merge (Step 1 / Step 2)
  - Excel → JSON
  - JSON → App
- ✅ Create a Google Sheet with predefined headers (including `status`)

---

## 1. Question Solving (Per Question)

For each practice question:

1. Send the question to ChatGPT using the **Question Solving Prompt**
2. From the response, extract:
   - `domainId`
   - `subdomainId`
   - **Final rule (written at a “10-year-old clarity” level)** → store as `rule_draft_10yo`
3. Add **one row per question** to the Sheet with:
   - `examId`
   - `domainId`
   - `subdomainId`
   - `question_id`
   - `rule_draft_10yo`
   - `status = draft`
4. Leave `triggers` / `pitfalls` empty at this stage if needed

---

## 2. Trigger & Pitfall Extraction (Every 10 Questions)

Purpose: extract signals **per question**, without early consolidation.

1. Copy the **full answer texts** for the 10 questions
2. Open a new chat window
3. Paste the **Per-Question Trigger & Pitfall Extraction Prompt**
4. Paste the 10-question text
5. The model outputs `triggers` and `pitfalls` **for each question individually**
6. Paste the outputs back into the corresponding rows in the Sheet  
   (duplicates are allowed)

---

## 3. Stabilization Decision (By Subdomain)

Within the same `subdomainId`:

- If a rule feels **automatic and consistently applicable**  
  → change `status` to `stable`
- If there is *any* hesitation:
  - Keep the rule as `draft`
  - Do **not** stabilize early

**Principle:**  
Prefer keeping more draft rules over premature merging.

---

## 4. Rule Merging (Two-Step Submission)

### Step 1: Merge Plan Only

1. Open a new chat window
2. Paste the **Two-Step Merge – Step 1 Prompt**
3. Paste the filtered Excel data  
   (recommended: export `.xlsx` and copy with headers)
4. The model outputs a **Merge Plan only** (no new table)

#### Self-check (must pass all 5):

- Did the row count change?
- Did any question IDs drift?
- Is the anchor still instantly applicable?
- Did any rule cross subdomains?
- Am I 100% confident in this merge?

---

### Step 2: Explicit Approval

- You reply with:
  “OK, generate final merged output.”
- The model outputs a **new merged table**:
- Sources merged
- Triggers / pitfalls unioned
- `status = stable`

---

## 5. Excel → JSON (Publishing Stage)

1. Filter the Sheet to include only `status = stable`
2. Paste the **Excel → JSON Prompt**
3. Paste the filtered data (with headers)
4. The model outputs JSON conforming to the schema:
 - `rule_draft_10yo` → `anchor`
 - `question_id` → `source`

This JSON is considered **publishable rule data**.

---

## 6. JSON → Workflow App (Implementation Stage)

1. Paste the **JSON → App Prompt**
2. Paste the published JSON
3. The App must support:
 - Displaying the anchor as a single concise rule
 - Using triggers to assist quick question scanning
 - Clickable / copyable source question IDs  
   (for returning to UWorld for re-practice)

---

## Guiding Principle

> **Human judgment defines rules.  
> AI assists with extraction and structure.  
> The workflow remains deterministic and auditable.**

  
