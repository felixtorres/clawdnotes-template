---
type: resource
tags: [dev, workflow, reference]
---

# Feature Development Workflow

A structured approach for developing features: from idea → PRD → DEV_PLAN → implementation.

## TL;DR

Every feature gets its own folder. Start with a PRD to define *what* and *why*. Once the approach is clear, create a DEV_PLAN for *how*. Then implement.

---

## Folder Structure

```
2-Projects/<project>/
├── README.md           # Project overview
├── tasks.md            # Cross-feature tasks
├── decisions.md        # Project-level ADRs
├── ideas.md            # Backlog of feature ideas
├── features/
│   └── <feature-name>/
│       ├── PRD.md          # What & why (required)
│       ├── DEV_PLAN.md     # How (after PRD approved)
│       ├── decisions.md    # Feature-specific ADRs (optional)
│       └── notes/          # Research, design docs (optional)
```

---

## Workflow Phases

### Phase 1: Idea Capture

**Location:** `ideas.md` in the project root

When a new feature idea emerges:
1. Add it to `ideas.md` with a brief description
2. Tag with priority/complexity if known
3. Link any related research or context

**Move to Phase 2 when:** The idea is worth exploring seriously.

---

### Phase 2: PRD (Product Requirements Document)

**Location:** `features/<feature-name>/PRD.md`

**Purpose:** Define *what* we're building and *why*.

**Template:** [[_templates/feature-prd]]

**Key sections:**
- Problem statement (what pain are we solving?)
- Proposed solution (high-level approach)
- Requirements (functional & non-functional)
- Acceptance criteria (how do we know it's done?)
- Out of scope (what we're NOT doing)

**PRD is complete when:**
- [ ] Problem is clearly articulated
- [ ] Solution approach is validated (research done)
- [ ] Requirements are specific and testable
- [ ] Stakeholder/self review complete

**Move to Phase 3 when:** PRD is approved and approach is clear.

---

### Phase 3: DEV_PLAN (Development Plan)

**Location:** `features/<feature-name>/DEV_PLAN.md`

**Purpose:** Define *how* we're building it.

**Template:** [[_templates/dev-plan]]

**Key sections:**
- Architecture/design decisions
- Implementation phases (ordered tasks)
- Technical specifications
- Testing strategy
- Dependencies and risks

**DEV_PLAN is complete when:**
- [ ] Architecture decisions documented
- [ ] Tasks are broken down and sequenced
- [ ] Testing approach defined
- [ ] Ready for implementation handoff

**Move to Phase 4 when:** DEV_PLAN is approved.

---

### Phase 4: Implementation

**Tracking:** Update `tasks.md` or use external issue tracker

During implementation:
1. Work through DEV_PLAN phases in order
2. Document decisions in `features/<feature>/decisions.md`
3. Add research/design notes to `features/<feature>/notes/`
4. Update PRD if requirements change (with changelog)

**Feature is complete when:**
- [ ] All acceptance criteria from PRD are met
- [ ] Tests pass
- [ ] Documentation updated
- [ ] Code reviewed/merged

---

## Feature Lifecycle

```
ideas.md → features/<name>/PRD.md → DEV_PLAN.md → Implementation → Complete
   │              │                      │              │
   │              ▼                      ▼              ▼
   │         Research              Architecture     Testing
   │         Validation            Design           Documentation
   ▼
 Backlog
```

### Status Tracking

Add status to PRD frontmatter:

```yaml
---
status: draft | review | approved | in-progress | complete | archived
---
```

### Archiving Completed Features

Options (pick one per project):
1. **Keep in place** - Add `status: complete` to PRD
2. **Move to archive** - `5-Archive/2-Projects/<project>/features/<feature>/`

---

## When to Skip Phases

**Small fixes/tweaks:** Skip PRD, just do it.

**Clear requirements:** Lightweight PRD (problem + acceptance criteria only).

**Prototype/spike:** PRD with `status: spike`, skip DEV_PLAN, document learnings.

---

## Templates

- [[_templates/feature-prd]] - PRD template
- [[_templates/dev-plan]] - Development plan template
