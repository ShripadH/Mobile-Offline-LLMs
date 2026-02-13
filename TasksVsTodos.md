# Task vs Todo – Stakeholder Comparison

## Executive Summary

**Todos improve individual productivity.**  
**Tasks ensure organizational control, workflow governance, and compliance.**

---

## 1. High-Level Comparison

| Dimension                 | Todo                      | Task                                                 |
| ------------------------- | ------------------------- | ---------------------------------------------------- |
| **Purpose**               | Personal reminder         | Business unit of work                                |
| **Scope**                 | Individual productivity   | Organizational workflow                              |
| **Ownership**             | Single user               | Assigned user + stakeholders                         |
| **Business Impact**       | Low                       | High / Operational                                   |
| **Compliance Relevance**  | None                      | Often regulatory-bound                               |
| **Audit Requirement**     | No                        | Yes (mandatory in banking)                           |
| **Workflow Complexity**   | Simple (Open → Done)      | Multi-state lifecycle                                |
| **Approval Required**     | No                        | Often yes                                            |
| **SLA Tracking**          | No                        | Yes                                                  |
| **Escalation Mechanism**  | No                        | Yes                                                  |
| **Client Association**    | Optional                  | Often mandatory                                      |
| **Risk Exposure**         | None                      | May carry financial / regulatory risk                |
| **Reporting & Metrics**   | Personal view             | Department / management dashboard                    |
| **Integration Needs**     | Minimal                   | CRM / Core banking / Compliance systems              |
| **Recurrence**            | Simple recurring reminder | Structured recurring compliance cycles               |
| **Dependencies**          | Rare                      | Can block or depend on other tasks                   |
| **Team Collaboration**    | Limited                   | Built-in collaboration                               |
| **State Model**           | `OPEN → DONE`             | `DRAFT → PENDING → IN_PROGRESS → REVIEW → COMPLETED` |
| **Data Model Complexity** | Lightweight               | Rich metadata structure                              |
| **Retention Policy**      | User-based                | Regulatory retention required                        |

---

## 2. Banking Scenario Examples

| Scenario                    | Todo | Task |
| --------------------------- | ---- | ---- |
| Call client for documents   | ✔    |      |
| Complete KYC verification   |      | ✔    |
| Submit AML alert review     |      | ✔    |
| Remember to check email     | ✔    |      |
| Loan approval workflow      |      | ✔    |
| Personal follow-up reminder | ✔    |      |

---

## 3. Lifecycle Comparison

### Todo Lifecycle

```text
OPEN → DONE
OPEN → SNOOZED → DONE


### Task Lifecycle
DRAFT
  ↓
PENDING
  ↓
IN_PROGRESS
  ↓
WAITING_ON_CLIENT / WAITING_ON_INTERNAL
  ↓
UNDER_REVIEW
  ↓
COMPLETED

Possible from any state:

CANCELLED


Derived State:

OVERDUE


```
