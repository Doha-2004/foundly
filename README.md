# FOUNDLY

### Validate. Trust. Match. Build Your Team.

Foundly is a trusted team-matching platform that helps project owners find qualified and available talents based on **validated skills, experience, availability, and project requirements**.

> **Foundly helps you find the right people before you start building the project.**

---

## Overview

Finding the right people for a project is often difficult.

People usually depend on LinkedIn, social media groups, messaging apps, personal networks, or freelancing platforms. However, these platforms do not always provide reliable information about a person's actual skill level or current availability.

Foundly introduces a **trust layer before team matching**.

Instead of relying only on self-declared skills, talents can validate their skills through standardized assessments and build a **Verified Talent Profile**.

Founders can then create projects, define their requirements, discover suitable talents, and form a qualified team.

---

## Core Concept

```text
Validate
    ↓
Trust
    ↓
Match
    ↓
Team
```

### Validate

Talents prove their skills through standardized assessments.

### Trust

Validated skills, experience, and availability provide better signals for decision-making.

### Match

Foundly compares project requirements with talent profiles.

### Team

Founders and talents connect through applications or invitations and form a team.

---

## Key Features

### For Talents

* Create a professional talent profile.
* Add skills and experience.
* Complete skill assessments.
* Obtain skill validation scores.
* Set availability status.
* Browse recommended projects.
* Search for suitable projects.
* Apply to projects.
* Receive project invitations.
* Accept or decline invitations.
* Join formed teams.

### For Founders

* Create projects.
* Define required skills.
* Set minimum validation scores.
* Define experience requirements.
* Specify team requirements.
* Discover recommended talents.
* Search and filter candidates.
* Compare candidates.
* Invite talents to projects.
* Review applications.
* Accept or reject applicants.
* Form project teams.

### For Administrators

* Manage users.
* Manage skills.
* Manage assessments.
* Manage question banks.
* Configure validation rules.
* Manage projects.
* Monitor applications and teams.
* View reports and analytics.
* Monitor audit logs.

---

## Skill Validation

Skill validation is one of Foundly's core mechanisms.

A talent does not simply claim:

```text
"I am a React Developer."
```

Instead, Foundly provides a standardized assessment process that generates a validation signal.

Example:

```text
React.js       91% ✓
JavaScript     88% ✓
HTML/CSS       94% ✓

Experience:
Intermediate

Availability:
Available
```

### Important

Validation does **not** guarantee real-world expertise.

It provides a standardized signal based on defined criteria to help founders make better-informed decisions.

---

## Assessment

The assessment system may include:

* Technical questions.
* Concepts.
* Debugging scenarios.
* Code scenarios.
* Best practices.
* Practical situations.
* Timed questions.
* Randomized questions.
* Randomized options.
* Fullscreen monitoring.
* Camera monitoring.
* Visibility/tab detection.
* Violation logging.
* Attempt limitations.

Foundly does not claim to completely prevent cheating.

Instead:

> **Foundly uses multiple mechanisms to reduce and detect suspicious exam behavior.**

---

## Matching

Foundly uses a rule-based matching approach for the MVP.

Example project requirements:

```text
React.js       ≥ 80%
JavaScript     ≥ 75%
Experience     ≥ Intermediate
Availability   = Available
```

Candidate:

```text
React.js       = 91%
JavaScript     = 88%
Experience     = Intermediate
Availability   = Available
```

Result:

```text
Strong Match
```

A configurable match score can consider:

| Factor       | Example Weight |
| ------------ | -------------: |
| Skills       |            40% |
| Validation   |            30% |
| Experience   |            20% |
| Availability |            10% |

> **Foundly recommends. The Founder decides.**

The match score is a recommendation, not an automatic decision.

---

## User Flow

### Talent

```text
Register
   ↓
Onboarding
   ↓
Assessment
   ↓
Validation
   ↓
Verified Profile
   ↓
Set Availability
   ↓
Browse Projects
   ↓
Apply
   ↓
Accepted
   ↓
Team Formed
```

### Founder

```text
Register
   ↓
Create Project
   ↓
Define Requirements
   ↓
Matching
   ↓
Recommended Talents
   ↓
Search / Filter / Compare
   ↓
Invite
   ↓
Talent Accepts
   ↓
Team Formed
```

---

## Team Formation

Foundly's primary responsibility ends when a qualified team is formed.

```text
Project
   ↓
Applications / Invitations
   ↓
Members Selected
   ↓
Team Created
   ↓
Your Team Is Ready
```

After team formation, members are free to use external tools such as:

* GitHub
* Discord
* WhatsApp
* Notion
* Trello
* Other collaboration tools

Foundly is **not** intended to replace project management or collaboration platforms.

---

## What Foundly Is Not

Foundly is not:

* ❌ LinkedIn
* ❌ A freelancing marketplace
* ❌ A funding platform
* ❌ A project management system
* ❌ A Trello/Notion alternative
* ❌ A complete startup workspace
* ❌ A platform for executing the entire project

### Scope Principle

> **Foundly stops at Team Formation.**

---

## MVP Scope

### Must Have

* Authentication
* User roles
* User profiles
* Skills
* Assessments
* Skill validation
* Availability
* Project creation
* Project requirements
* Matching
* Search and filtering
* Applications
* Invitations
* Accept / Reject
* Team formation
* Admin dashboard

### Should Have

* Notifications
* Realtime updates
* Team group
* Analytics
* Email verification
* Validation renewal

### Nice to Have

* Advanced proctoring
* Advanced analytics
* Premium subscriptions
* B2B portal
* Advanced recommendation algorithms

---

## Technology Stack

### Frontend

* React.js / Next.js
* Tailwind CSS

### Backend

* ASP.NET Core Web API

### Database

* SQL Server

### Authentication

* JWT
* Refresh Tokens
* Google Login

### Realtime Communication

* SignalR

### Storage

* Cloudinary

### Deployment

* Docker
* Azure

---

## High-Level Architecture

```text
                  FOUNDLY
                     │
          ┌──────────┴──────────┐
          │                     │
      Frontend               Backend
 React / Next.js         ASP.NET Core API
          │                     │
          │             ┌───────┴────────┐
          │             │                │
          │        Business Logic   Authentication
          │             │                │
          │             └───────┬────────┘
          │                     │
          └─────────────────────┤
                                │
                           SQL Server
                                │
                    ┌───────────┴───────────┐
                    │                       │
                Cloudinary                SignalR
```

---

## Core Entities

```text
User
Role
Skill
UserSkill

Assessment
Question
AssessmentQuestion
AssessmentAttempt
AssessmentAnswer

SkillValidation

Project
ProjectSkillRequirement

Application
Invitation

Team
TeamMember

Availability
Notification
AuditLog
```

Optional communication entities:

```text
Conversation
ConversationMember
Message
```

---

## Security

Because Foundly handles assessments and user data, security is a core requirement.

The system is expected to implement:

* JWT authentication.
* Refresh tokens.
* Role-based authorization.
* Password hashing.
* Email verification.
* Forgot password.
* Rate limiting.
* Input validation.
* Server-side exam timing.
* Attempt limitations.
* Concurrent exam prevention.
* Audit logs.
* Secure APIs.

---

## Product Principle

Every new feature should be evaluated against the Foundly DNA:

```text
        VALIDATE
            ↓
          TRUST
            ↓
          MATCH
            ↓
           TEAM
```

Before adding a feature, ask:

> **Does this feature directly support Validate, Trust, Match, or Team Formation?**

If not, it should generally remain outside the MVP.

---

## Core USP

> **Foundly adds a trust layer to team matching through standardized skill validation and availability-aware matching.**

In simple terms:

> **The problem is not just finding people. The problem is knowing who is suitable and trustworthy enough to build a team with.**

---

## One-Sentence Description

> **Foundly is a trusted team-matching platform that validates users' skills and matches qualified, available talents with project owners based on project requirements.**

---

## Foundly DNA

# Validate → Trust → Match → Team

**Validate** — Prove your skills.
**Trust** — Provide reliable signals about your capabilities.
**Match** — Find people who fit the project's requirements.
**Team** — Form a qualified team and move forward.

---

## Project Status

**Status:** MVP Development

Foundly is currently focused on building the core team-formation experience:

```text
Skill Validation
      ↓
Verified Profiles
      ↓
Availability
      ↓
Project Requirements
      ↓
Matching
      ↓
Applications / Invitations
      ↓
Team Formation
```

---

## License

This project is currently under development.

License and usage terms will be defined by the project owners.
