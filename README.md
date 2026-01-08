# CPA Workflow Engine

A rule-based workflow engine for CPA exam question classification and decision support.

---

## What This Is

This project is a **decision-support workflow**, built to help CPA candidates quickly identify **which judgment framework applies** to a given multiple-choice question.

Instead of summarizing content or explaining textbook theory, the engine focuses on **how to decide**, not **what to memorize**.

---

## What Problem It Solves

During high-volume practice, many mistakes come from applying the **wrong judgment logic**, not from missing knowledge.

This workflow helps answer three questions:

1. Which domain does this question belong to?
2. Which subdomain does it fall into?
3. Which judgment rule should be applied?

---

## How It Works (Conceptually)

Key signal
↓
Domain classification
↓
Secondary signal
↓
Subdomain classification
↓
Judgment anchor


Each judgment anchor consists of:
- One concise rule
- Common pitfalls
- Source references for review

---

## What This Is Not

- Not a textbook replacement
- Not a content summary
- Not an AI recommendation system
- Not an automated scoring or explanation tool

This is a **transparent, rule-based workflow**, designed for real practice use.

---

## Why This Matters

This project demonstrates the ability to:
- Break down complex judgment tasks into explicit workflows
- Design reusable, auditable decision rules
- Translate real practice experience into structured systems

---

## Project Status

This repository contains the **workflow engine layer**:
- Rule schema
- Prompts and extraction workflow
- Documentation for rule validation and iteration

Client applications (e.g. mobile apps) will consume the exported rule data but remain separate from this repository.

---

For detailed workflow design and engineering rationale, see:
- `docs/workflow_design.md`
