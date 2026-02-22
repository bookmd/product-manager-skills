# User Flow Spec: [Product Name]

**Date:** [YYYY-MM-DD]
**Roles:** [Role 1, Role 2, ...]
**Scenarios:** [count] scenarios across [count] screens

---

## Constraints

- **Navigation:** [sidebar / tabs / top-nav / other]
- **Framework:** [React / Vue / other / none specified]
- **Target:** [desktop-first / mobile-first / responsive]
- **Component library:** [library name / none specified]
- **Design guidelines:** [any specific conventions]
- **Out of scope:** [screens or flows excluded]

---

## Screen Registry

| ID   | Screen Name | Status | Scenarios |
|------|-------------|--------|-----------|
| S-01 | [name]      | [ ]    | [SC-x]    |
| S-02 | [name]      | [ ]    | [SC-x]    |

**Progress:** 0/[N] screens spec'd

---

## Scenario Flows

### SC-1: [Scenario name — Role: verb + goal]

S-01 → S-02 → S-03 → S-01

**Branch points:**
- At S-03, if [condition] → S-04 (alternate path)

---

## Screen Specs

### S-01: [Screen Name]

**Wireframe:**

```
┌─────────────────────────────────────────────┐
│  [header]                                   │
├──────────┬──────────────────────────────────┤
│ [nav]    │  [content]                       │
│          │                                  │
└──────────┴──────────────────────────────────┘
```

**Elements:**
- [Element] — [type: button/field/table/indicator] — [data source]

**States:**
- **Loading:** [description]
- **Empty:** [description + CTA if applicable]
- **Populated:** [description]
- **Error:** [description]

**Transitions:**
- `[action]` → S-XX ([Screen Name])
