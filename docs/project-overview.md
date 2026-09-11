# FOUNDLY — Project Overview

> **Validate → Trust → Match → Team**

## 1. Introduction

**Foundly** is a trusted team-matching platform designed to help project owners and idea owners find qualified and available people to build their teams.

Instead of relying only on self-declared skills, Foundly introduces a **trust layer** through standardized skill validation, experience information, and availability status.

The platform connects:

* **Founders / Idea Owners** who need people for their projects.
* **Talents** who have skills and want to join projects and teams.

Foundly focuses on one core problem:

> **Finding the right people you can trust before starting a project.**

Foundly is responsible for helping users **validate skills, discover suitable people, and form a team**.

It is not intended to manage the project after the team has been formed.

---

## 2. Vision

To make team formation more reliable by helping people discover qualified, validated, and available talents based on actual project requirements.

---

## 3. Mission

Foundly aims to reduce the uncertainty involved in building project teams by providing:

* Standardized skill validation.
* Verified talent profiles.
* Availability-aware matching.
* Project-specific requirements.
* Structured applications and invitations.
* A clear team formation process.

---

## 4. Problem Statement

People with project ideas often struggle with one fundamental question:

> **"Who should I work with?"**

Building a team usually requires finding people with different skills, such as:

* Frontend Development
* Backend Development
* Mobile Development
* UI/UX Design
* Artificial Intelligence
* Marketing
* Business
* Other technical and non-technical skills

Currently, people may search for team members through:

* LinkedIn
* Facebook Groups
* WhatsApp
* Discord
* Freelancing platforms
* Personal networks
* Friends and colleagues

However, these approaches have several limitations.

### 4.1 Self-Declared Skills

Users can claim skills without providing standardized evidence of their proficiency.

For example:

```text
React
JavaScript
Node.js
Python
```

may appear on a profile without providing a reliable indication of the user's actual level.

### 4.2 Lack of Standardized Validation

There is usually no common validation mechanism that allows a project owner to understand how strong a candidate is in a specific skill.

### 4.3 Unclear Availability

A suitable candidate may already be working with another team or may not currently be available.

### 4.4 Fragmented Information

Project owners often need to collect information from multiple platforms before deciding whether someone is suitable.

---

## 5. Proposed Solution

Foundly introduces a **Trust Layer Before Team Matching**.

The core process is:

```text
User
  ↓
Skill & Experience Validation
  ↓
Verified Profile
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

Instead of relying only on what a user claims about their skills, Foundly provides additional signals such as:

```text
React.js        91% Validated
JavaScript      88% Validated
Experience      Intermediate
Availability    Available
```

This allows project owners to make better-informed decisions.

---

## 6. Core Value Proposition

Foundly's value is not simply matching people.

The platform adds a **trust layer** to the matching process.

### Core Value Proposition

> **Foundly validates skills and matches qualified, available talents with project owners based on project requirements.**

The core product philosophy is:

```text
Validate
    ↓
Trust
    ↓
Match
    ↓
Team
```

---

## 7. Core USP

### English

> **Foundly adds a trust layer to team matching through standardized skill validation and availability-aware matching.**

### Arabic

> **Foundly مش بس بتجمع الناس ببعض، لكنها بتضيف طبقة ثقة من خلال التحقق من المهارات وربطها بالـavailability واحتياجات المشروع.**

The key difference is:

> **The problem is not only finding people. The problem is knowing whether they are suitable and trustworthy for the team.**

---

## 8. Target Users

Foundly primarily serves two user types.

### 8.1 Founder / Idea Owner

A person who has a project idea and needs qualified people to form a team.

Example:

```text
Project:
EduConnect

Required Team:

- React Developer
- Backend Developer
- UI/UX Designer
```

The Founder can define project requirements and discover candidates who meet them.

---

### 8.2 Talent

A person with skills and experience who wants to join projects or teams.

Example:

```text
Name:
Doha

Role:
Frontend Developer

Experience:
Intermediate

Verified Skills:

React.js       91%
JavaScript     88%
HTML/CSS       94%

Availability:
Available
```

The Talent can:

* Complete skill assessments.
* Build a verified profile.
* Set availability.
* Browse projects.
* Apply to projects.
* Receive invitations.
* Join teams.

---

## 9. User Roles

The platform contains three primary roles:

### Talent

Responsible for:

* Creating a profile.
* Providing experience information.
* Completing assessments.
* Obtaining skill validations.
* Managing availability.
* Browsing projects.
* Applying to projects.
* Accepting or declining invitations.
* Joining teams.

### Founder

Responsible for:

* Creating projects.
* Defining project requirements.
* Searching for talents.
* Filtering candidates.
* Reviewing candidate profiles.
* Inviting talents.
* Accepting or rejecting applications.
* Forming teams.

### Admin

Responsible for managing and monitoring the platform.

The Admin can:

* Manage users.
* Manage skills.
* Manage assessments.
* Manage question banks.
* Configure validation rules.
* Monitor projects.
* View analytics.
* Monitor audit logs.
* Manage platform-level settings.

---

## 10. Core Features

### 10.1 Skill Validation

Talents can complete assessments to validate their skills.

Validation may include:

* Technical knowledge.
* Concepts.
* Debugging.
* Code scenarios.
* Best practices.
* Practical situations.

The resulting validation score becomes part of the user's verified profile.

---

### 10.2 Verified Talent Profile

A talent profile contains relevant information such as:

* Profile picture.
* Name.
* Short bio.
* Experience level.
* Skills.
* Validation scores.
* Availability.
* Validation expiration date.

The profile is designed to provide useful information without becoming a complete public CV or personal directory.

---

### 10.3 Availability

Talents can indicate their current availability:

```text
Available
Currently in a Team
Not Available
```

When a talent joins a team, their availability can automatically change from:

```text
Available
    ↓
Currently in a Team
```

This helps prevent multiple founders from selecting someone who is no longer available.

---

### 10.4 Project Creation

Founders can create projects and define requirements such as:

* Project name.
* Category.
* Team size.
* Required skills.
* Minimum validation score.
* Required experience level.
* Availability requirements.
* Short project description.

---

### 10.5 Matching

Foundly uses a rule-based matching system to compare project requirements with talent profiles.

Example:

```text
Required:

React ≥ 80%
JavaScript ≥ 75%
Experience ≥ Intermediate
Availability = Available
```

Candidate:

```text
React = 91%
JavaScript = 88%
Experience = Intermediate
Availability = Available
```

Result:

```text
Strong Match
```

---

### 10.6 Match Score

The platform can calculate a match score using configurable factors.

Example:

| Factor       | Weight |
| ------------ | -----: |
| Skills       |    40% |
| Validation   |    30% |
| Experience   |    20% |
| Availability |    10% |

The weights should be configurable rather than hard-coded.

The resulting score is a recommendation signal, not a final decision.

> **Foundly recommends. Founder decides.**

---

### 10.7 Applications

Talents can apply to suitable projects.

Example:

```text
Doha
    ↓
Applied to EduConnect
    ↓
Status: Pending
```

The Founder can then:

```text
Accept
Reject
```

---

### 10.8 Invitations

Founders can directly invite suitable talents.

Example:

```text
Founder
    ↓
Invite Talent
    ↓
Talent receives notification
    ↓
Accept / Decline
```

---

### 10.9 Team Formation

After the required members accept applications or invitations:

```text
Project
   ↓
Members Selected
   ↓
Team Created
```

The team may contain:

```text
Founder
Frontend Developer
Backend Developer
UI/UX Designer
```

At this point, Foundly has completed its primary responsibility.

---

## 11. Assessment System

Assessment is one of Foundly's core mechanisms.

The purpose is not to guarantee that someone is an expert.

Instead, it provides a **standardized validation signal** that helps project owners make better-informed decisions.

### Assessment Flow

```text
Assessment Instructions
        ↓
System Check
        ↓
Fullscreen
        ↓
Camera Permission
        ↓
Timed Assessment
        ↓
Questions
        ↓
Submission
        ↓
Evaluation
        ↓
Validation Result
```

The system may use:

* Timed questions.
* Randomized questions.
* Randomized options.
* Fullscreen monitoring.
* Camera monitoring.
* Visibility/tab detection.
* Violation logging.
* Limited attempts.

The platform should not claim that cheating is completely prevented.

Instead:

> **Foundly uses multiple mechanisms to reduce and detect suspicious exam behavior.**

---

## 12. Validation Levels

Validation levels can be configured by the Admin.

Example:

|   Score | Level        |
| ------: | ------------ |
|  60–69% | Basic        |
|  70–84% | Intermediate |
| 85–100% | Advanced     |

These values are examples and should be configurable.

A validation may also have an expiration period.

Example:

```text
Validated:
September 2026

Valid Until:
September 2027
```

After expiration, the user may need to complete a renewal assessment.

---

## 13. Project Privacy

Founders do not necessarily need to expose the complete details of their ideas publicly.

A project can provide a high-level description such as:

> **Educational platform looking for a frontend and backend team.**

while exposing requirements such as:

```text
Required Skills:

React.js
ASP.NET Core
UI/UX

Minimum React Validation:
80%
```

Sensitive project details can be revealed later according to the platform's business rules.

---

## 14. What Foundly Is Not

To maintain a focused product scope, Foundly is **not**:

* A LinkedIn replacement.
* A freelancing marketplace.
* A funding platform.
* A project management system.
* A Trello or Notion alternative.
* A complete startup workspace.
* A platform for executing the entire project.

Foundly's responsibility is:

> **Formation of a qualified team.**

Once the team is formed, members are free to use external tools such as:

* GitHub
* Discord
* WhatsApp
* Notion
* Trello
* Other collaboration tools

---

## 15. MVP Scope

The MVP focuses on the core product journey.

### Must Have

* Authentication.
* User roles.
* User profiles.
* Skills.
* Assessments.
* Skill validation.
* Availability.
* Project creation.
* Project requirements.
* Matching.
* Search and filtering.
* Applications.
* Invitations.
* Accept / Reject.
* Team formation.
* Admin dashboard.

### Should Have

* Notifications.
* Realtime updates.
* Team group.
* Analytics.
* Email verification.
* Validation renewal.

### Nice to Have

* Advanced proctoring.
* Advanced analytics.
* Premium subscriptions.
* B2B portal.
* Advanced recommendation algorithms.

---

## 16. Scope Boundary

The following are intentionally outside the core MVP:

```text
Funding
Project Management
Task Management
Kanban Boards
File Management
Meeting Management
Full Workspace
Complete Project Execution
```

The fundamental scope rule is:

> **Foundly stops at Team Formation.**

Any future feature should be evaluated against this principle.

---

## 17. Product Decision Rule

When considering a new feature, the team should ask:

> **Does this feature directly support Validate, Trust, Match, or Team Formation?**

If the answer is no, the feature should generally not be included in the Foundly MVP.

### Foundly DNA

```text
VALIDATE
    ↓
TRUST
    ↓
MATCH
    ↓
TEAM
```

---

## 18. Competitive Positioning

### Foundly vs LinkedIn

LinkedIn focuses on:

```text
Connect → Network → Search
```

Foundly focuses on:

```text
Validate → Verify → Match → Form Team
```

The key difference is **trust and team formation**.

---

### Foundly vs GitHub

GitHub is primarily focused on code collaboration.

Foundly starts earlier:

> **Who should be on the team?**

---

### Foundly vs Trello / Notion

Trello and Notion focus on:

> **Managing work.**

Foundly focuses on:

> **Finding the people to do the work.**

---

### Foundly vs Co-Founder Matching Platforms

Traditional co-founder matching focuses primarily on connecting potential co-founders.

Foundly can differentiate itself through:

* Standardized skill validation.
* Validation scores.
* Multiple skill categories.
* Availability.
* Project-specific requirements.
* Team formation beyond only co-founder matching.

---

## 19. Business Model Overview

Foundly can generate revenue through multiple streams.

### Skill Validation

Users may pay for different validation levels.

The value is based on:

> **Validation Level + Trust + Visibility**

rather than simply the number of questions.

---

### Talent Premium

Premium features may include:

* Advanced search.
* More applications.
* Higher profile visibility.
* Advanced validation options.
* Analytics.
* Profile boost.

---

### Founder Premium

Premium features may include:

* Advanced matching.
* Verified-only candidates.
* Advanced filters.
* More invitations.
* Larger candidate pool.
* Candidate comparison.

---

### B2B

Potential organization customers include:

* Universities.
* Training centers.
* Hackathons.
* Incubators.
* Companies.

Possible use cases include:

* Student skill validation.
* Trainee assessment.
* Participant verification.
* Team formation.
* Talent assessment.

---

## 20. Business Flywheel

The Foundly business model can be represented as:

```text
More Validated Talents
        ↓
Better Matching
        ↓
More Successful Teams
        ↓
More Founders
        ↓
More Projects
        ↓
More Talents
        ↓
More Revenue
```

As the number of validated talents increases, the value of the platform can increase as well.

---

## 21. Trust Loop

The product's core mechanism can also be represented as:

```text
Assessment
    ↓
Validation
    ↓
Verified Profile
    ↓
Better Matching
    ↓
Team Formation
    ↓
User Experience
    ↓
Renewal / Premium
```

This makes assessment more than a feature.

It becomes a core business mechanism.

---

## 22. Key Risks

### 22.1 Assessment Does Not Guarantee Real-World Expertise

The assessment cannot prove that a person is an expert in every real-world situation.

Foundly should communicate this clearly:

> **The assessment does not guarantee real-world expertise. It provides a standardized validation signal based on defined criteria, helping founders make better-informed decisions.**

---

### 22.2 Users May Move Communication Outside Foundly

Foundly does not need to prevent users from communicating through external platforms.

Once a qualified team has been formed, users can use:

* WhatsApp
* Discord
* GitHub
* Notion
* Trello
* Other tools

The core value has already been delivered:

> **Foundly helped qualified people find each other and form a team.**

---

### 22.3 Scope Expansion

A major product risk is continuously adding features such as:

* Tasks.
* Files.
* Meetings.
* Project management.
* Funding.
* Complex integrations.

These features can transform Foundly into a completely different product.

The MVP should therefore remain focused on:

```text
Validate
Trust
Match
Team Formation
```

---

## 23. Technology Overview

The planned technology stack is:

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

### Realtime

* SignalR

### Storage

* Cloudinary

### Deployment

* Docker
* Azure

---

## 24. High-Level Architecture

```text
                    FOUNDLY
                       │
        ┌──────────────┴──────────────┐
        │                             │
   Frontend                       Backend
React / Next.js              ASP.NET Core API
        │                             │
        │                    ┌────────┴────────┐
        │                    │                 │
        │                Business Logic    Authentication
        │                    │                 │
        │                    └────────┬────────┘
        │                             │
        └─────────────────────────────┤
                                      │
                                  SQL Server
                                      │
                         ┌────────────┴────────────┐
                         │                         │
                     Cloudinary                 SignalR
```

---

## 25. Core Entities

The main system entities include:

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

Optional entities for team communication:

```text
Conversation
ConversationMember
Message
```

---

## 26. Main User Flows

### Talent Flow

```text
Register
   ↓
Onboarding
   ↓
Assessment
   ↓
Pass
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

### Founder Flow

```text
Register
   ↓
Create Project
   ↓
Define Requirements
   ↓
Matching Engine
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

## 27. One-Sentence Description

> **Foundly is a trusted team-matching platform that validates users' skills and matches qualified, available talents with project owners based on project requirements.**

### Short Version

> **Foundly helps people build qualified teams through skill validation, trusted profiles, and availability-aware matching.**

---

## 28. Foundly in Four Words

# Validate → Trust → Match → Team

**Validate**
Prove your skills.

**Trust**
Give others reliable signals about your capabilities.

**Match**
Find people who fit the project's requirements.

**Team**
Form a qualified team and move forward.

---

## 29. Final Product Principle

Foundly is not trying to become another platform that does everything.

Its purpose is simple:

> **Help the right people find each other and form a qualified team with more confidence.**

Everything inside the MVP should support one or more of these four principles:

```text
VALIDATE
TRUST
MATCH
TEAM
```

**Foundly stops at Team Formation.**
