# Workflow Design – CPA Workflow Engine

## Purpose

This document describes the internal design philosophy and workflow behind the CPA Workflow Engine.

It focuses on **how decision rules are extracted, validated, and stabilized**, rather than on implementation details or user interfaces.

---

## Design Goal

The goal of this system is to formalize **implicit human judgment** into **explicit, reusable decision rules**, without delegating decision authority to automation or AI.

Human reasoning remains the source of truth throughout the workflow.

---

## Core Design Principles

### 1. Workflow First

The workflow is defined and frozen before any application or UI is built.

Tools exist only to support the workflow, not to redefine it.

---

### 2. Rule Transparency

Every decision must map to a clear rule:
- Short
- Deterministic
- Human-readable

No rule is treated as a black box.

---

### 3. Separation of Concerns

- This repository owns **rule generation and validation**
- Client applications only **consume published rule data**

Rule logic and presentation logic are intentionally decoupled.

---

## Rule Structure

Each rule includes:

- Domain and subdomain classification
- A concise judgment anchor (plain language)
- Triggers (signals that help identify applicability)
- Common pitfalls (frequent misinterpretations)
- Source identifiers for review

Rules are treated as **data**, not executable code.

---

## End-to-End Workflow

### Step 1: Question Analysis

Each question is analyzed manually to identify:
- Domain
- Subdomain
- Initial judgment logic

A draft rule is written in simple language.

---

### Step 2: Signal Extraction

Triggers and pitfalls are extracted **per question**, not merged prematurely.

This avoids early overgeneralization.

---

### Step 3: Stabilization

Rules are marked as *stable* only when they:
- Generalize across multiple questions
- Can be applied confidently without hesitation

Uncertain rules remain in draft state.

---

### Step 4: Two-Step Merge

Rule consolidation follows a strict two-step process:

1. Generate a merge plan for review
2. Explicit approval before producing merged rules

This ensures correctness over convenience.

---

### Step 5: Publishing

Stable rules are exported into structured JSON:
- Conforming to a fixed schema
- Ready for direct consumption by applications

---

## Non-Goals

This workflow explicitly avoids:
- Automated rule generation
- AI-based recommendations
- Probabilistic scoring
- Knowledge explanation engines

The system exists to **support judgment**, not replace it.

---

## Evolution Strategy

Rules evolve through real usage:
- New questions validate or challenge existing rules
- Rules are refined, merged, or deprecated as needed
- Schema changes are versioned and minimal

The workflow is designed to remain stable even as content grows.

---

## Summary

This project treats decision-making as a system design problem.

By externalizing judgment logic into explicit workflows, it aims to reduce cognitive load, improve consistency, and make complex decision processes auditable and reusable.
