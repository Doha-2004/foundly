# Foundly — Software Requirements Specification (SRS)


## 1. Introduction

Foundly is a web platform that validates people's skills and matches qualified, available talents with project owners, and it stops once a team is formed. This SRS is written for a junior development team and can be turned into an ERD, SQL tables, API docs and tasks.

### 1.1 Project Name

Foundly — *Validate → Trust → Match → Team*.

### 1.2 Purpose of the System

People with project ideas struggle to answer "Who should I work with?". Today they search LinkedIn, Facebook groups, WhatsApp, Discord and personal networks, where skills are self-declared, there is no standard validation, availability is unclear and information is scattered. Foundly adds a **trust layer** before matching: standardized skill assessments, experience level and availability status.

### 1.3 Scope

| In scope (MVP) | Out of scope |
| --- | --- |
| Authentication, roles, profiles | Funding |
| Skills, assessments, skill validation | Project management, tasks, Kanban boards |
| Availability status | File and meeting management |
| Project creation and requirements | Full startup workspace |
| Rule-based matching, search and filtering | Executing the project after the team is formed |
| Applications, invitations, accept / reject | Replacing LinkedIn or acting as a freelancing marketplace |
| Team formation |  |
| Admin dashboard |  |

Scope rule: **Foundly stops at Team Formation.** Any new feature must directly support Validate, Trust, Match or Team Formation.

### 1.4 Objectives

| ID | Objective | Measure |
| --- | --- | --- |
| OBJ-1 | Let talents prove skills through standardized assessments | A talent can finish an assessment and receive a validation score and level |
| OBJ-2 | Give founders reliable talent profiles | Every profile shows validated skills, experience, availability and expiry date |
| OBJ-3 | Match talents to project requirements | The founder sees a ranked list with a match score for each project |
| OBJ-4 | Avoid selecting unavailable people | Availability changes to "Currently in a Team" automatically when a talent joins a team |
| OBJ-5 | Form teams through a clear process | Applications and invitations end in Accepted or Rejected / Declined, and accepted members form a team |
| OBJ-6 | Let admins control the platform | Admins manage users, skills, question banks, validation rules and audit logs |

### 1.5 Target Users

| User | Description |
| --- | --- |
| Founder / Idea Owner | Has a project idea and needs qualified people (for example, a React developer, a backend developer and a UI/UX designer for a project called EduConnect) |
| Talent | Has skills and experience and wants to join projects or teams (for example, a frontend developer with validated React, JavaScript and HTML/CSS skills) |
| Admin | Manages and monitors the platform |

## 2. Overall Description

Foundly is a new, standalone web product with a React/Next.js frontend, an ASP.NET Core API and a SQL Server database. It covers the journey from skill validation to team formation only.

### 2.1 Product Perspective

The core process the system supports is:

1. User registers and completes onboarding.
2. User takes a skill assessment (Talent) or creates a project (Founder).
3. System creates a validated skill record and a verified profile.
4. Talent sets availability; Founder defines project requirements.
5. The matching engine compares requirements with profiles and calculates a match score.
6. Founder invites talents, or talents apply to projects.
7. The other side accepts or rejects.
8. Accepted members form a team and the system updates their availability.

**Guiding principle:** Foundly recommends, the Founder decides. A match score is a recommendation signal, never a final decision.

External systems used: Google (login), Cloudinary (image storage), email service (verification and notifications), Azure (hosting).

### 2.2 Product Features

| No. | Feature | Short description | Priority |
| --- | --- | --- | --- |
| F1 | Authentication and roles | Register, log in (email or Google), JWT with refresh tokens, role-based access | High |
| F2 | Profiles | Talent and Founder profiles with bio, picture and experience level | High |
| F3 | Skill management | Admin-managed skill catalog; Talents choose skills | High |
| F4 | Assessments | Timed, randomized exams with monitoring and limited attempts | High |
| F5 | Skill validation | Score, level, expiry date and renewal | High |
| F6 | Availability | Available / Currently in a Team / Not Available | High |
| F7 | Project creation | Projects with requirements per skill | High |
| F8 | Matching and match score | Rule-based matching with configurable weights | High |
| F9 | Search and filtering | Founders search talents; Talents browse projects | High |
| F10 | Applications | Talent applies; Founder accepts or rejects | High |
| F11 | Invitations | Founder invites; Talent accepts or declines | High |
| F12 | Team formation | Team and members created from accepted requests | High |
| F13 | Admin dashboard | Users, skills, question banks, rules, projects, analytics, audit logs | High |
| F14 | Notifications and realtime | In-app notifications via SignalR | Medium |
| F15 | Email verification | Verify email after registration | Medium |
| F16 | Team group chat (optional) | Simple conversation for team members | Low |

### 2.3 User Types and Roles

| Role | Summary |
| --- | --- |
| Talent | Builds a verified profile, takes assessments, sets availability, applies to projects, answers invitations, joins teams |
| Founder | Creates projects, defines requirements, searches and compares talents, invites, reviews applications, forms teams |
| Admin | Manages platform data and rules, monitors projects, analytics and audit logs |

One user account has exactly one primary role. Full permissions are in section 4.

### 2.4 Operating Environment

| Layer | Technology |
| --- | --- |
| Frontend | React.js / Next.js, Tailwind CSS |
| Backend | ASP.NET Core Web API |
| Database | SQL Server |
| Authentication | JWT, refresh tokens, Google Login |
| Realtime | SignalR |
| Storage | Cloudinary |
| Deployment | Docker on Azure |
| Client | Latest versions of Chrome, Edge, Firefox and Safari on desktop and mobile; camera required for assessments |

### 2.5 Assumptions and Dependencies

- Users have a stable internet connection, a modern browser and (for assessments) a working camera.
- Question banks are prepared by Admins before assessments are offered for a skill.
- Google, Cloudinary, Azure and an email provider are available and configured.
- Users communicate through external tools (WhatsApp, Discord, GitHub, Notion, Trello) after a team is formed.
- Scoring bands, expiry periods and match weights are configuration values, not fixed in code.

### 2.6 Constraints

- The system must not include project management, tasks, files, meetings or funding.
- The platform must not claim that assessments prevent cheating completely or guarantee real-world expertise; it must state that assessments are a standardized validation signal.
- Talent profiles must not become a full public CV or personal directory.
- The listed technology stack must be used.
- Project details marked sensitive must stay hidden until the platform's rules allow revealing them.

## 3. Functional Requirements

The system has 35 functional requirements (FR-001 to FR-035). Each one lists its ID, name, description, inputs, process, outputs, validation rules and priority. Priorities: High = MVP must have, Medium = should have, Low = nice to have.

### 3.1 Authentication and Access

#### FR-001 — User Registration (High)

- **Description:** A new visitor creates an account as Talent or Founder.
- **Inputs:** Full name, email, password, confirm password, role (Talent or Founder).
- **Process:** Validate input → check email is unused → hash password → create User with selected Role → create an empty profile → send verification email (FR-004).
- **Outputs:** Account created; user is signed in or sent to login; success message.
- **Validation:** Email must be valid and unique. Password is at least 8 characters with an uppercase letter, a lowercase letter and a digit. Passwords must match. Admin role cannot be chosen at registration.

#### FR-002 — User Login (High)

- **Description:** A registered user signs in with email and password or with Google.
- **Inputs:** Email and password, or a Google token.
- **Process:** Verify credentials → check account is active → issue a JWT access token and a refresh token → record the login in the audit log.
- **Outputs:** Access token, refresh token, user role and basic profile data.
- **Validation:** Wrong credentials return a generic error (do not reveal which field is wrong). Blocked accounts cannot log in. After 5 failed attempts the account is locked for 15 minutes.

#### FR-003 — Token Refresh and Logout (High)

- **Description:** Keep the user signed in safely and allow sign-out.
- **Inputs:** Refresh token.
- **Process:** Check the refresh token is valid, not expired and not revoked → issue a new access token (and rotate the refresh token). On logout, revoke the refresh token.
- **Outputs:** New tokens, or confirmation of logout.
- **Validation:** Expired, revoked or reused refresh tokens are rejected and the user must log in again.

#### FR-004 — Email Verification (Medium)

- **Description:** Users confirm they own their email address.
- **Inputs:** Verification token from the email link; or a request to resend it.
- **Process:** Validate the token → mark the email as verified → allow resending if needed.
- **Outputs:** Verified status; confirmation message.
- **Validation:** Token expires after 24 hours and works once. Resend is limited to 3 requests per hour. Unverified users cannot take assessments, apply, or send invitations.

#### FR-005 — Role-Based Access Control (High)

- **Description:** Every page and API action is limited by role.
- **Inputs:** JWT with the user's role.
- **Process:** The API checks the role for each request; the frontend hides pages the role cannot use.
- **Outputs:** Allowed action, or a 403 error.
- **Validation:** Users can only read and change their own data unless their role allows more (see section 4).

### 3.2 Profiles, Skills and Question Banks

#### FR-006 — Talent Profile and Onboarding (High)

- **Description:** A Talent builds a profile that shows verified information without becoming a full CV.
- **Inputs:** Profile picture, name, short bio, main role (for example Frontend Developer), experience level (Beginner, Intermediate, Advanced).
- **Process:** Save profile → upload picture to Cloudinary → show the profile with validated skills, validation scores, availability and expiry dates.
- **Outputs:** Talent profile page; profile completion status.
- **Validation:** Name is required (max 100 characters). Bio is max 300 characters. Picture is JPG or PNG, max 2 MB. No phone number, address or full work history fields are stored.

#### FR-007 — Founder Profile (High)

- **Description:** A Founder keeps a short profile that talents can see.
- **Inputs:** Picture, name, short bio.
- **Process:** Save and display profile.
- **Outputs:** Founder profile page.
- **Validation:** Same limits as FR-006.

#### FR-008 — Skill Catalog Management (High)

- **Description:** The Admin manages the list of skills (for example React.js, JavaScript, ASP.NET Core, UI/UX, Marketing).
- **Inputs:** Skill name, category (Technical or Non-technical), description, active flag.
- **Process:** Create, edit or deactivate a skill. Deactivated skills cannot be used in new projects or assessments, but existing validations stay.
- **Outputs:** Updated skill list.
- **Validation:** Skill name is unique (case-insensitive). A skill with linked data cannot be deleted, only deactivated.

#### FR-009 — Talent Skill Selection (High)

- **Description:** A Talent chooses the skills they want to validate and show.
- **Inputs:** Skill ID.
- **Process:** Add the skill to the Talent's list with status "Not Validated" → the Talent can start an assessment for it. After validation the status becomes "Validated".
- **Outputs:** Talent skill list with validation status.
- **Validation:** Only active skills can be added. A skill can be added once per Talent. A skill that is not validated is clearly labeled "Not Validated" and is not used for matching.

#### FR-010 — Question Bank Management (High)

- **Description:** The Admin creates and maintains questions for each skill.
- **Inputs:** Skill ID, question text, question type (concept, debugging, code scenario, best practice, practical situation), difficulty, 2–6 options, correct option, active flag.
- **Process:** Create, edit, deactivate and list questions; filter by skill and difficulty.
- **Outputs:** Updated question bank.
- **Validation:** Each question has exactly one correct option. A skill needs at least as many active questions as its assessment requires before it can be assessed.

### 3.3 Assessments and Skill Validation

#### FR-011 — Assessment Configuration (High)

- **Description:** The Admin sets the rules for each skill's assessment.
- **Inputs:** Skill ID, number of questions, time limit (minutes), pass score, maximum attempts, retake wait time (hours), validation level bands, validity period (months), monitoring switches (fullscreen, camera, tab detection).
- **Process:** Save the configuration; new attempts use the latest configuration, and attempts already started keep the old one.
- **Outputs:** Saved assessment configuration.
- **Validation:** Pass score is 0–100. Level bands must not overlap and must cover 60–100 (default: 60–69 Basic, 70–84 Intermediate, 85–100 Advanced). Time limit and question count must be greater than 0.

#### FR-012 — Start Assessment (High)

- **Description:** A Talent begins an assessment after reading the rules and passing a system check.
- **Inputs:** Skill ID; acceptance of the rules; camera permission.
- **Process:** Show instructions (including the note that the assessment is a validation signal, not a guarantee of expertise) → system check → request fullscreen → request camera permission → create an Assessment Attempt with randomly chosen questions and randomized option order → start the timer.
- **Outputs:** Active attempt with the first question and a countdown timer.
- **Validation:** The Talent must be verified by email, must have added the skill, must not exceed the attempt limit, must wait out the retake period, and must not have another active attempt. If camera or fullscreen is denied, the attempt does not start.

#### FR-013 — Answer Questions and Submit (High)

- **Description:** The Talent answers timed questions and submits the assessment.
- **Inputs:** Selected option for each question; submit action.
- **Process:** Save each answer as it is chosen → allow navigation between questions → submit manually or automatically when the timer ends.
- **Outputs:** Submission confirmation.
- **Validation:** The server decides the time, not the browser. Answers sent after the deadline are ignored. A submitted attempt cannot be changed.

#### FR-014 — Monitoring and Violation Logging (High)

- **Description:** The system uses several mechanisms to reduce and detect suspicious behavior. It does not claim to prevent cheating completely.
- **Inputs:** Browser events: exit fullscreen, tab or window switch, camera lost, page reload.
- **Process:** Record each event as a violation with time and type → warn the Talent → after the configured number of violations (default 3), auto-submit and flag the attempt for review.
- **Outputs:** Violation records visible to the Admin; warning messages to the Talent.
- **Validation:** Each violation is saved with attempt ID and timestamp. Flagged attempts are marked "Under Review" and do not create a validation until the Admin approves.

#### FR-015 — Evaluation and Validation Result (High)

- **Description:** The system scores the attempt and creates the skill validation.
- **Inputs:** Submitted attempt.
- **Process:** Compare answers with correct options → calculate percentage score → compare with the pass score → find the level → create or update the Skill Validation with score, level, validated date and expiry date.
- **Outputs:** Result page with score, level and expiry date; the verified skill appears on the profile (for example, "React.js 91% Validated").
- **Validation:** Score = correct answers ÷ total questions × 100, rounded to a whole number. A failed attempt creates no validation. A newer passed result replaces the previous validation for the same skill.

#### FR-016 — Validation Expiry and Renewal (Medium)

- **Description:** Validations expire and can be renewed.
- **Inputs:** Validation expiry date; renewal assessment.
- **Process:** A daily job marks expired validations → the skill returns to "Expired" and is excluded from matching → send a reminder 30 days before expiry → a new passed assessment creates a new validity period.
- **Outputs:** Updated status (Validated, Expired); notifications.
- **Validation:** Expired validations are shown on the profile as "Expired" and never count in match score.

### 3.4 Availability and Projects

#### FR-017 — Availability Management (High)

- **Description:** A Talent sets whether they can join a new team.
- **Inputs:** Status: Available, Currently in a Team, Not Available.
- **Process:** Talent updates status manually; the system sets "Currently in a Team" automatically when the Talent joins a team (FR-030).
- **Outputs:** Updated status on the profile and in search results.
- **Validation:** Only "Available" talents can receive new invitations or have applications accepted. A Talent in a team can change status back only by leaving the team or by Admin action.

#### FR-018 — Project Creation (High)

- **Description:** A Founder creates a project to find team members.
- **Inputs:** Project name, category, short description, team size (number of members needed, 2–20), status.
- **Process:** Save project in Draft → Founder adds requirements (FR-019) → Founder publishes the project.
- **Outputs:** Project page; project status (Draft, Open, Team Formed, Closed).
- **Validation:** Name is required and max 100 characters. Description is max 500 characters. A project can only be published with at least one skill requirement. Only the owner can edit or close it.

#### FR-019 — Project Skill Requirements (High)

- **Description:** The Founder defines who the project needs.
- **Inputs:** For each needed position: skill, minimum validation score, required experience level, availability requirement (default Available), number of openings.
- **Process:** Add, edit or remove requirements while the project is Draft or Open.
- **Outputs:** Requirement list used by matching.
- **Validation:** Minimum score is 0–100. The skill must be active. The total number of openings cannot be greater than team size minus one (the Founder is a member).

#### FR-020 — Project Privacy (Medium)

- **Description:** Founders do not have to expose the full idea publicly.
- **Inputs:** Public summary; private details; visibility setting.
- **Process:** Show only the public summary and requirements to Talents → reveal private details only to accepted team members.
- **Outputs:** Different project views for public visitors, applicants and team members.
- **Validation:** Private details are never returned by the API to non-members.

### 3.5 Matching and Search

#### FR-021 — Rule-Based Matching (High)

- **Description:** The system compares a project's requirements with talent profiles and finds suitable talents.
- **Inputs:** Project ID (all requirements of that project).
- **Process:** For each requirement, select talents who have the skill with a non-expired validation, a score at or above the minimum, an experience level at or above the required level, and the required availability → calculate a match score (FR-022) → classify the result → return a ranked list.
- **Outputs:** Ranked talents per requirement with match score and a label: Strong Match (80–100), Good Match (60–79), Partial Match (40–59). Talents under 40 are not recommended.
- **Validation:** Only active talents with a verified email appear. Unvalidated or expired skills never count. The result is a recommendation; the Founder makes the decision.

#### FR-022 — Match Score and Configurable Weights (High)

- **Description:** A weighted score ranks candidates. Weights are settings, not hard-coded values.
- **Inputs:** Admin weights (default: Skills 40%, Validation 30%, Experience 20%, Availability 10%).
- **Process:** Calculate each factor as a 0–100 value (see rule BR-12) and apply the formula below.
- **Outputs:** Match score from 0 to 100 and a breakdown by factor.
- **Validation:** Weights must be 0 or more and add up to exactly 100%. Changes are saved in the audit log.

Match Score = (Skills × Wₛ) + (Validation × Wᵥ) + (Experience × Wₑ) + (Availability × Wₐ)

#### FR-023 — Search and Filter Talents (High)

- **Description:** A Founder searches the talent pool.
- **Inputs:** Keyword, skill, minimum validation score, experience level, availability, validation level; sort option; page number.
- **Process:** Filter and sort talents → return a page of results with a short profile card.
- **Outputs:** Paged list of verified talent cards.
- **Validation:** Default page size is 20. Only validated, non-expired skills are used by the score filters. Search never returns email, phone or private data.

#### FR-024 — Compare Candidates (Medium)

- **Description:** A Founder compares 2–4 candidates side by side.
- **Inputs:** List of 2–4 Talent IDs; project ID (optional).
- **Process:** Load their validated skills, levels, experience, availability and match score for the project.
- **Outputs:** Comparison table.
- **Validation:** Minimum 2 and maximum 4 candidates.

#### FR-025 — Browse and Filter Projects (High)

- **Description:** A Talent browses open projects and sees how well they fit.
- **Inputs:** Keyword, category, skill, availability need; page number.
- **Process:** Return open projects with public summary and requirements → show the Talent's match score for each.
- **Outputs:** Paged project list.
- **Validation:** Only projects with status Open are shown. Private details are hidden (FR-020).

### 3.6 Applications, Invitations and Team Formation

#### FR-026 — Apply to a Project (High)

- **Description:** A Talent applies to an open position.
- **Inputs:** Project ID, requirement ID, short message (optional).
- **Process:** Create an Application with status Pending → notify the Founder.
- **Outputs:** Application with status Pending.
- **Validation:** The Talent must have status Available, a verified email, and a non-expired validation for the required skill. A Talent can have only one Pending application per requirement. The Talent cannot apply to the Talent's own project or to a closed project.

#### FR-027 — Review Applications (High)

- **Description:** A Founder accepts or rejects applications.
- **Inputs:** Application ID, decision (Accept or Reject), reason (optional).
- **Process:** Update the status → notify the Talent → if accepted, add the Talent to the pending member list of the project.
- **Outputs:** Application status Accepted or Rejected.
- **Validation:** Only the project owner can decide. Only Pending applications can be decided. Accepting is blocked if the opening is already full or the Talent is no longer Available.

#### FR-028 — Send Invitation (High)

- **Description:** A Founder invites a suitable Talent directly.
- **Inputs:** Project ID, requirement ID, Talent ID, message (optional).
- **Process:** Create an Invitation with status Pending and an expiry date (default 7 days) → notify the Talent.
- **Outputs:** Invitation with status Pending.
- **Validation:** The Talent must be Available. No duplicate Pending invitation for the same Talent and requirement. The Founder cannot send more invitations than the openings still free plus a limit of 10 open invitations per project.

#### FR-029 — Respond to Invitation (High)

- **Description:** A Talent accepts or declines an invitation.
- **Inputs:** Invitation ID, decision (Accept or Decline).
- **Process:** Update the status → notify the Founder → if accepted, add the Talent to the pending member list.
- **Outputs:** Invitation status Accepted or Declined.
- **Validation:** Only the invited Talent can respond. Expired invitations cannot be accepted. Accepting is blocked if the Talent is no longer Available or the opening is full.

#### FR-030 — Team Formation (High)

- **Description:** Accepted members become a team. This is the last step Foundly manages.
- **Inputs:** Project ID; Founder confirms the team.
- **Process:** Create the Team → add the Founder and accepted members as Team Members with their positions → set each Talent's availability to Currently in a Team → close the matching openings → cancel remaining Pending applications and invitations of those Talents → set project status to Team Formed → notify members.
- **Outputs:** Team with its member list.
- **Validation:** The Founder can confirm when at least one opening has been filled. All members must still be Available at confirmation. The steps run in one database transaction.

### 3.7 Notifications, Administration and Team Chat

#### FR-031 — Notifications and Realtime Updates (Medium)

- **Description:** Users are told about important events instantly.
- **Inputs:** System events: new application, application decision, new invitation, invitation response, team formed, validation expiring.
- **Process:** Save a Notification → push it through SignalR if the user is online → show unread count.
- **Outputs:** Notification list; mark as read.
- **Validation:** A user only sees their own notifications. Notifications older than 90 days are removed.

#### FR-032 — Admin User Management (High)

- **Description:** The Admin manages user accounts.
- **Inputs:** Search keyword, user ID, action (block, unblock, change role, reset availability).
- **Process:** Apply the action → log it in the audit log.
- **Outputs:** Updated user record.
- **Validation:** An Admin cannot block or demote their own account. Every action needs a reason text.

#### FR-033 — Admin Project Monitoring and Analytics (Medium)

- **Description:** The Admin watches platform activity.
- **Inputs:** Date range; filters.
- **Process:** Calculate counts and rates from existing data.
- **Outputs:** Dashboard with: registered users by role, assessments taken and pass rate by skill, validated talents, open and completed projects, applications and invitations accepted rate, teams formed. The Admin can also close an inappropriate project.
- **Validation:** Dates must be valid and the start is before the end.

#### FR-034 — Audit Log (High)

- **Description:** Important actions are recorded and can be searched by the Admin.
- **Inputs:** Filters: user, action type, date range.
- **Process:** The system writes a record for login, role change, block, configuration change, assessment violation, application and invitation decisions, and team formation.
- **Outputs:** Paged read-only log.
- **Validation:** Audit records cannot be edited or deleted by anyone through the application.

#### FR-035 — Team Group Chat (Low, optional)

- **Description:** Team members get one simple group conversation after formation.
- **Inputs:** Message text.
- **Process:** Create a Conversation when the team is formed → members send and read messages through SignalR.
- **Outputs:** Message list.
- **Validation:** Only team members can read or write. Message length is max 1000 characters. This feature must stay simple: no files, tasks or meetings.

## 4. User Roles and Permissions

There are three signed-in roles (Talent, Founder, Admin) plus the Guest, who is not signed in. Each account has one role.

### 4.1 Roles, Permissions and Accessible Pages

| Role | Permissions | Accessible pages |
| --- | --- | --- |
| Guest | View landing page; register; log in; verify email | Landing, Register, Login, Verify Email |
| Talent | Edit own profile; choose skills; take assessments (within attempt limits); view own results; set availability; browse and filter open projects; apply; withdraw own applications; answer invitations; view own team; view notifications | Talent Dashboard, My Profile, My Skills, Assessment Instructions, Assessment Room, Assessment Result, Browse Projects, Project Details, My Applications, My Invitations, My Team, Notifications, Settings |
| Founder | Edit own profile; create, edit, publish and close own projects; define requirements; view recommended talents; search, filter and compare talents; view talent profiles; send invitations; accept or reject applications; confirm team formation; view own teams; view notifications | Founder Dashboard, My Profile, My Projects, Create / Edit Project, Project Requirements, Recommended Talents, Talent Search, Talent Profile View, Compare Candidates, Applications Review, Sent Invitations, My Team, Notifications, Settings |
| Admin | Manage users (block, unblock, change role); manage skills, question banks and assessment rules; set match weights; review flagged attempts; monitor and close projects; view analytics; view audit logs; manage platform settings | Admin Dashboard, Users, Skills, Question Bank, Assessment Rules, Attempt Review, Projects Monitor, Analytics, Audit Logs, Platform Settings |

### 4.2 Permission Matrix by Action

Y = allowed, N = not allowed, Own = only on the user's own data.

| Action | Guest | Talent | Founder | Admin |
| --- | --- | --- | --- | --- |
| Register / log in | Y | N | N | N |
| Edit profile | N | Own | Own | Own |
| Take assessment | N | Y | N | N |
| Set availability | N | Own | N | Reset any |
| Create project | N | N | Y | N |
| Edit / close project | N | N | Own | Close any |
| Browse open projects | N | Y | Y | Y |
| Search talents | N | N | Y | Y |
| Apply to project | N | Y | N | N |
| Accept / reject application | N | N | Own projects | N |
| Send invitation | N | N | Y | N |
| Accept / decline invitation | N | Own | N | N |
| Confirm team | N | N | Own projects | N |
| Manage skills and question banks | N | N | N | Y |
| Configure rules and weights | N | N | N | Y |
| View audit logs and analytics | N | N | N | Y |

A Founder who also wants to join a team as a Talent needs a separate account in the MVP.

## 5. Use Cases

There are 17 use cases covering the full journey. Alternative flows (A1, A2…) branch from the main-flow step shown.

#### UC-01 — Register and Verify Account

- **Actor:** Guest
- **Description:** A visitor creates a Talent or Founder account and confirms the email. (FR-001, FR-004)
- **Preconditions:** The visitor has no account with this email.
- **Main flow:** 1) Open Register. 2) Enter name, email, password and role. 3) System validates and creates the account. 4) System sends a verification email. 5) User clicks the link. 6) System marks the email as verified.
- **Alternative flow:** A1 (step 3) Email exists or password is weak → show an error, stay on the form. A2 (step 5) Link expired → user requests a new link.
- **Postconditions:** An active, verified account with the chosen role and an empty profile exists.

#### UC-02 — Log In

- **Actor:** Talent, Founder, Admin
- **Description:** A user signs in and is sent to the dashboard of their role. (FR-002, FR-003, FR-005)
- **Preconditions:** The user has an active account.
- **Main flow:** 1) Open Login. 2) Enter email and password, or choose Google. 3) System checks credentials. 4) System issues tokens. 5) System opens the role dashboard.
- **Alternative flow:** A1 (step 3) Wrong credentials → generic error. A2 (step 3) 5 failed attempts → account locked for 15 minutes. A3 Account blocked → message to contact support.
- **Postconditions:** The user is signed in; the login is in the audit log.

#### UC-03 — Complete Talent Profile and Choose Skills

- **Actor:** Talent
- **Description:** A Talent adds profile data and the skills to validate. (FR-006, FR-009)
- **Preconditions:** The Talent is signed in.
- **Main flow:** 1) Open Onboarding. 2) Enter bio, picture, main role and experience level. 3) Pick skills from the catalog. 4) Save.
- **Alternative flow:** A1 (step 2) Picture too large or wrong type → error. A2 Talent skips skills → can add them later.
- **Postconditions:** Profile is saved; selected skills show "Not Validated".

#### UC-04 — Take a Skill Assessment

- **Actor:** Talent
- **Description:** A Talent takes a timed, monitored assessment for one skill. (FR-012 to FR-015)
- **Preconditions:** Email verified; skill added; attempts remain; retake wait time passed; skill has enough questions.
- **Main flow:** 1) Choose the skill and read the instructions. 2) Pass the system check. 3) Allow fullscreen and camera. 4) System creates the attempt with random questions and starts the timer. 5) Talent answers questions. 6) Talent submits. 7) System scores the attempt and creates the validation. 8) System shows score, level and expiry date.
- **Alternative flow:** A1 (step 3) Permission denied → attempt does not start. A2 (step 5) Violation → warning and log. A3 Violations reach the limit → auto-submit and flag for review. A4 (step 5) Timer ends → auto-submit. A5 (step 7) Score below pass mark → no validation; show the retake date.
- **Postconditions:** The attempt is saved. On a pass, a Skill Validation exists with score, level and expiry.

#### UC-05 — Renew an Expiring Validation

- **Actor:** Talent
- **Description:** A Talent renews a validation that is expiring or expired. (FR-016)
- **Preconditions:** A validation exists that is expired or within 30 days of expiry.
- **Main flow:** 1) Talent receives a reminder. 2) Opens My Skills. 3) Selects Renew. 4) Completes UC-04. 5) System replaces the validation and sets a new expiry date.
- **Alternative flow:** A1 (step 4) Talent fails → old validation stays until its expiry date.
- **Postconditions:** The validation is active with a new expiry date, or unchanged.

#### UC-06 — Set Availability

- **Actor:** Talent
- **Description:** A Talent changes availability status. (FR-017)
- **Preconditions:** The Talent is signed in and is not in a team (or wants to change within allowed values).
- **Main flow:** 1) Open Profile. 2) Choose Available or Not Available. 3) Save.
- **Alternative flow:** A1 Talent is Currently in a Team → status cannot be changed manually.
- **Postconditions:** The new status appears on the profile and in search results.

#### UC-07 — Create a Project with Requirements

- **Actor:** Founder
- **Description:** A Founder creates a project and defines the needed positions. (FR-018 to FR-020)
- **Preconditions:** The Founder is signed in and verified.
- **Main flow:** 1) Open Create Project. 2) Enter name, category, public summary, private details, team size. 3) Save as Draft. 4) Add requirements (skill, minimum score, experience, openings). 5) Publish.
- **Alternative flow:** A1 (step 5) No requirement → publishing blocked. A2 Founder leaves → draft stays saved.
- **Postconditions:** The project is Open and visible to Talents with its public summary.

#### UC-08 — View Recommended Talents

- **Actor:** Founder
- **Description:** The system shows ranked talents for each requirement. (FR-021, FR-022)
- **Preconditions:** The Founder owns an Open project with requirements.
- **Main flow:** 1) Open the project. 2) Select Recommended Talents. 3) System runs matching. 4) System shows ranked talents with match score and label.
- **Alternative flow:** A1 (step 4) No talent qualifies → show a message and suggest lowering a minimum score.
- **Postconditions:** No data changes. The Founder decides what to do next.

#### UC-09 — Search, Filter and Compare Talents

- **Actor:** Founder
- **Description:** A Founder explores the talent pool manually. (FR-023, FR-024)
- **Preconditions:** The Founder is signed in.
- **Main flow:** 1) Open Talent Search. 2) Apply filters. 3) Open profiles. 4) Select 2–4 talents. 5) Open Compare.
- **Alternative flow:** A1 (step 4) More than 4 selected → show an error.
- **Postconditions:** No data changes.

#### UC-10 — Invite a Talent

- **Actor:** Founder
- **Description:** A Founder invites a talent to fill a position. (FR-028)
- **Preconditions:** The project is Open; the position has a free opening; the Talent is Available.
- **Main flow:** 1) Open the Talent profile. 2) Choose Invite and select the project and position. 3) Add an optional message. 4) System creates a Pending invitation. 5) System notifies the Talent.
- **Alternative flow:** A1 (step 4) Duplicate Pending invitation → error. A2 (step 4) Talent is no longer Available → error.
- **Postconditions:** An invitation with status Pending and an expiry date exists.

#### UC-11 — Respond to an Invitation

- **Actor:** Talent
- **Description:** A Talent accepts or declines an invitation. (FR-029)
- **Preconditions:** A Pending, non-expired invitation exists for the Talent.
- **Main flow:** 1) Talent opens My Invitations. 2) Reads the project summary and position. 3) Chooses Accept. 4) System updates the status and notifies the Founder.
- **Alternative flow:** A1 Talent chooses Decline → status Declined; Founder is notified. A2 Invitation expired → system shows Expired. A3 (step 3) Opening already full → error.
- **Postconditions:** Invitation is Accepted, Declined or Expired.

#### UC-12 — Apply to a Project

- **Actor:** Talent
- **Description:** A Talent applies to a position. (FR-025, FR-026)
- **Preconditions:** The Talent is Available with a non-expired validation for the required skill; the project is Open.
- **Main flow:** 1) Open Browse Projects. 2) Open a project. 3) Choose a position and Apply. 4) Add an optional message. 5) System creates a Pending application and notifies the Founder.
- **Alternative flow:** A1 (step 3) Missing validation → show a link to take the assessment. A2 Duplicate application → error.
- **Postconditions:** An application with status Pending exists.

#### UC-13 — Review an Application

- **Actor:** Founder
- **Description:** A Founder accepts or rejects an application. (FR-027)
- **Preconditions:** A Pending application exists on the Founder's project.
- **Main flow:** 1) Open Applications Review. 2) Open the Talent's profile. 3) Choose Accept. 4) System updates the status and notifies the Talent.
- **Alternative flow:** A1 Founder chooses Reject → status Rejected; Talent is notified. A2 (step 3) Talent no longer Available → system blocks accepting.
- **Postconditions:** The application is Accepted or Rejected.

#### UC-14 — Form a Team

- **Actor:** Founder
- **Description:** The Founder confirms the accepted members as a team. (FR-030, FR-017)
- **Preconditions:** At least one invitation or application is Accepted; all accepted members are Available.
- **Main flow:** 1) Open the project. 2) Review the member list. 3) Choose Confirm Team. 4) System creates the Team and Team Members. 5) System sets members to Currently in a Team. 6) System cancels their other Pending requests. 7) System sets the project to Team Formed and notifies members.
- **Alternative flow:** A1 (step 3) A member became unavailable → system lists the member and asks the Founder to remove them. A2 Some openings are unfilled → the Founder can confirm now or keep the project Open.
- **Postconditions:** A Team exists. Foundly's responsibility is complete.

#### UC-15 — Manage Skills, Question Bank and Assessment Rules

- **Actor:** Admin
- **Description:** The Admin prepares what assessments need. (FR-008, FR-010, FR-011, FR-022)
- **Preconditions:** The Admin is signed in.
- **Main flow:** 1) Open Skills and add or edit a skill. 2) Open Question Bank and add questions. 3) Open Assessment Rules and set time, pass score, levels, validity and attempts. 4) Open Platform Settings and set match weights. 5) Save.
- **Alternative flow:** A1 Weights do not add up to 100% → error. A2 Not enough questions → the skill cannot be assessed yet.
- **Postconditions:** Configuration is saved and logged.

#### UC-16 — Review a Flagged Attempt

- **Actor:** Admin
- **Description:** The Admin decides on an attempt flagged for violations. (FR-014)
- **Preconditions:** A flagged attempt exists.
- **Main flow:** 1) Open Attempt Review. 2) View violations and the score. 3) Choose Approve or Reject. 4) System creates a validation (approve) or discards the result (reject).
- **Alternative flow:** A1 Admin rejects → Talent is notified and may retake after the wait time.
- **Postconditions:** The attempt status is Approved or Rejected; the decision is logged.

#### UC-17 — Monitor the Platform

- **Actor:** Admin
- **Description:** The Admin reviews analytics, projects, users and audit logs. (FR-032 to FR-034)
- **Preconditions:** The Admin is signed in.
- **Main flow:** 1) Open Admin Dashboard. 2) Choose a date range. 3) Review the charts. 4) Open Users, Projects Monitor or Audit Logs. 5) Take an action if needed (block a user, close a project).
- **Alternative flow:** A1 No data in range → show an empty state.
- **Postconditions:** Any action taken is saved and logged.

## 6. Non-Functional Requirements

Every requirement below is measurable so it can be tested.

| ID | Category | Requirement |
| --- | --- | --- |
| NFR-001 | Performance | 95% of API requests (except matching and search) respond in under 500 ms with 500 concurrent users |
| NFR-002 | Performance | Matching for one project returns in under 2 seconds with 10,000 talents |
| NFR-003 | Performance | Search results return in under 1 second; lists are paged (default 20 items) |
| NFR-004 | Performance | Pages load in under 3 seconds on a 4G connection (first meaningful content) |
| NFR-005 | Performance | Notifications arrive through SignalR within 2 seconds of the event |
| NFR-006 | Security | Passwords are stored only as salted hashes (for example ASP.NET Identity hasher or BCrypt); never in plain text or logs |
| NFR-007 | Security | All traffic uses HTTPS; access tokens expire after 15 minutes; refresh tokens after 7 days and are rotated |
| NFR-008 | Security | Every endpoint checks the role and ownership on the server; the frontend check is only for display |
| NFR-009 | Security | All inputs are validated on the server; queries use parameters (no SQL injection); output is encoded (no XSS); CORS allows only the Foundly frontend |
| NFR-010 | Security | Login and verification endpoints are rate-limited (for example 10 requests per minute per IP) |
| NFR-011 | Security | Correct answers and private project details are never sent to clients that should not see them |
| NFR-012 | Security | Camera access is used only for monitoring during an assessment; the system states what is recorded and keeps it according to the privacy policy |
| NFR-013 | Usability | A new Talent can reach the first assessment within 5 minutes of registering without help |
| NFR-014 | Usability | Every form shows clear field-level error messages; every list has loading, empty and error states |
| NFR-015 | Availability | Target uptime is 99.5% per month, not counting planned maintenance announced 24 hours before |
| NFR-016 | Availability | Database backups run daily and can be restored within 4 hours; assessment answers are saved as chosen so a connection loss does not lose them |
| NFR-017 | Scalability | The API is stateless so that several containers can run behind a load balancer; SignalR can use a backplane |
| NFR-018 | Scalability | The design supports 50,000 users and 1 million assessment answers with proper indexes (see section 7) |
| NFR-019 | Maintainability | Code follows a layered structure (API, Business Logic, Data Access) with dependency injection |
| NFR-020 | Maintainability | Business logic has at least 70% unit-test coverage; matching and scoring have tests for each rule |
| NFR-021 | Maintainability | Database changes use migrations; API is documented with Swagger / OpenAPI; settings (weights, levels, limits) live in the database or config |
| NFR-022 | Maintainability | Errors and important events are logged with a correlation ID |
| NFR-023 | Compatibility | Works on the latest two versions of Chrome, Edge, Firefox and Safari; works on Android and iOS browsers |
| NFR-024 | Compatibility | Assessments require a browser that supports fullscreen and camera APIs; unsupported browsers see a clear message |
| NFR-025 | Accessibility | Follows WCAG 2.1 level AA: color contrast at least 4.5:1, keyboard navigation for all actions, visible focus, alt text for images, labels for form fields |
| NFR-026 | Accessibility | Status (for example Available or Expired) is never shown by color alone; text or an icon is also used |

## 7. Database Requirements

The database is SQL Server with 29 tables. Names are singular PascalCase and can be used directly as SQL table names. Primary keys are `INT IDENTITY` unless stated. Every table also has `CreatedAt` (DATETIME2, default current UTC time) unless it is a pure link table. PK = primary key, FK = foreign key, UQ = unique.

### 7.1 List of Entities

| # | Entity | Purpose | PK | Foreign keys |
| --- | --- | --- | --- | --- |
| 1 | Role | Talent, Founder, Admin | RoleId | — |
| 2 | User | Account | UserId | RoleId |
| 3 | RefreshToken | Refresh tokens | RefreshTokenId | UserId |
| 4 | EmailVerificationToken | Email verification links | TokenId | UserId |
| 5 | Profile | Bio, picture, experience | UserId | UserId |
| 6 | Availability | Current availability | AvailabilityId | UserId |
| 7 | Skill | Skill catalog | SkillId | — |
| 8 | UserSkill | Skills a Talent selected | UserSkillId | UserId, SkillId |
| 9 | Assessment | Assessment rules per skill | AssessmentId | SkillId |
| 10 | ValidationLevel | Score bands per assessment | ValidationLevelId | AssessmentId |
| 11 | Question | Question bank | QuestionId | SkillId, CreatedBy |
| 12 | QuestionOption | Answer options | OptionId | QuestionId |
| 13 | AssessmentQuestion | Questions that belong to an assessment | (AssessmentId, QuestionId) | AssessmentId, QuestionId |
| 14 | AssessmentAttempt | One try by a Talent | AttemptId | UserId, AssessmentId, ReviewedBy |
| 15 | AssessmentAnswer | One answer in an attempt | AnswerId | AttemptId, QuestionId, SelectedOptionId |
| 16 | AttemptViolation | Suspicious events | ViolationId | AttemptId |
| 17 | SkillValidation | Result that appears on the profile | ValidationId | UserId, SkillId, AttemptId, ValidationLevelId |
| 18 | Project | Founder's project | ProjectId | OwnerId |
| 19 | ProjectSkillRequirement | Needed position and its rules | RequirementId | ProjectId, SkillId |
| 20 | Application | Talent applies | ApplicationId | RequirementId, TalentId |
| 21 | Invitation | Founder invites | InvitationId | RequirementId, TalentId, FounderId |
| 22 | Team | Team of a project | TeamId | ProjectId |
| 23 | TeamMember | Members of a team | TeamMemberId | TeamId, UserId, RequirementId |
| 24 | Notification | In-app notifications | NotificationId | UserId |
| 25 | AuditLog | Important actions | AuditLogId | UserId |
| 26 | SystemSetting | Weights and limits | SettingKey | UpdatedBy |
| 27 | Conversation | Team chat (optional) | ConversationId | TeamId |
| 28 | ConversationMember / Message | Chat members and messages (two tables) | (ConversationId, UserId) / MessageId | ConversationId, UserId / ConversationId, SenderId |

### 7.2 Attributes

#### Identity and profile

**Role**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| RoleId | INT | PK |
| Name | NVARCHAR(20) | UQ; Talent, Founder, Admin |

**User**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| UserId | INT | PK |
| RoleId | INT | FK → Role |
| FullName | NVARCHAR(100) | Required |
| Email | NVARCHAR(256) | UQ, required |
| PasswordHash | NVARCHAR(256) | Null for Google-only accounts |
| GoogleId | NVARCHAR(100) | UQ, null |
| IsEmailVerified | BIT | Default 0 |
| IsActive | BIT | Default 1; 0 = blocked |
| FailedLoginCount | INT | Default 0 |
| LockoutEnd | DATETIME2 | Null |

**RefreshToken**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| RefreshTokenId | INT | PK |
| UserId | INT | FK → User |
| TokenHash | NVARCHAR(256) | UQ |
| ExpiresAt | DATETIME2 | Required |
| RevokedAt | DATETIME2 | Null |
| ReplacedByTokenId | INT | FK → RefreshToken, null |

**EmailVerificationToken**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| TokenId | INT | PK |
| UserId | INT | FK → User |
| TokenHash | NVARCHAR(256) | UQ |
| ExpiresAt | DATETIME2 | Required |
| UsedAt | DATETIME2 | Null |

**Profile** (one per user)

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| UserId | INT | PK and FK → User |
| Bio | NVARCHAR(300) | Null |
| PictureUrl | NVARCHAR(500) | Cloudinary URL, null |
| MainRole | NVARCHAR(100) | Null; for example Frontend Developer |
| ExperienceLevel | TINYINT | 1 Beginner, 2 Intermediate, 3 Advanced; null for Founders |
| UpdatedAt | DATETIME2 | Required |

**Availability** (one per Talent)

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| AvailabilityId | INT | PK |
| UserId | INT | FK → User, UQ |
| Status | TINYINT | 1 Available, 2 Currently in a Team, 3 Not Available |
| UpdatedAt | DATETIME2 | Required |

#### Skills and assessments

**Skill**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| SkillId | INT | PK |
| Name | NVARCHAR(100) | UQ |
| Category | NVARCHAR(50) | Technical or Non-technical |
| Description | NVARCHAR(500) | Null |
| IsActive | BIT | Default 1 |

**UserSkill**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| UserSkillId | INT | PK |
| UserId | INT | FK → User |
| SkillId | INT | FK → Skill |
| Status | TINYINT | 1 Not Validated, 2 Validated, 3 Expired |
| — | — | UQ (UserId, SkillId) |

**Assessment** (the rules for one skill; one active row per skill)

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| AssessmentId | INT | PK |
| SkillId | INT | FK → Skill |
| Title | NVARCHAR(150) | Required |
| QuestionCount | INT | Greater than 0 |
| TimeLimitMinutes | INT | Greater than 0 |
| PassScore | INT | 0–100 |
| MaxAttempts | INT | Greater than 0 |
| RetakeWaitHours | INT | 0 or more |
| ValidityMonths | INT | Greater than 0 |
| RequireFullscreen / RequireCamera / DetectTabSwitch | BIT | Default 1 |
| MaxViolations | INT | Default 3 |
| IsActive | BIT | Default 1 |

**ValidationLevel**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| ValidationLevelId | INT | PK |
| AssessmentId | INT | FK → Assessment |
| Name | NVARCHAR(30) | Basic, Intermediate, Advanced |
| MinScore / MaxScore | INT | 0–100; bands must not overlap |

**Question**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| QuestionId | INT | PK |
| SkillId | INT | FK → Skill |
| Text | NVARCHAR(1000) | Required |
| Type | TINYINT | 1 Concept, 2 Debugging, 3 Code scenario, 4 Best practice, 5 Practical |
| Difficulty | TINYINT | 1 Easy, 2 Medium, 3 Hard |
| IsActive | BIT | Default 1 |
| CreatedBy | INT | FK → User (Admin) |

**QuestionOption**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| OptionId | INT | PK |
| QuestionId | INT | FK → Question |
| Text | NVARCHAR(500) | Required |
| IsCorrect | BIT | Exactly one true per question |

**AssessmentQuestion** (link table)

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| AssessmentId | INT | PK part, FK → Assessment |
| QuestionId | INT | PK part, FK → Question |

**AssessmentAttempt**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| AttemptId | INT | PK |
| UserId | INT | FK → User (Talent) |
| AssessmentId | INT | FK → Assessment |
| StartedAt | DATETIME2 | Required |
| DeadlineAt | DATETIME2 | StartedAt + time limit |
| SubmittedAt | DATETIME2 | Null |
| Status | TINYINT | 1 In Progress, 2 Submitted, 3 Under Review, 4 Approved, 5 Rejected |
| Score | INT | 0–100, null until scored |
| Passed | BIT | Null until scored |
| ViolationCount | INT | Default 0 |
| ReviewedBy | INT | FK → User (Admin), null |
| ReviewedAt | DATETIME2 | Null |

**AssessmentAnswer**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| AnswerId | INT | PK |
| AttemptId | INT | FK → AssessmentAttempt |
| QuestionId | INT | FK → Question |
| SelectedOptionId | INT | FK → QuestionOption, null until answered |
| DisplayOrder | INT | Random order for this attempt |
| IsCorrect | BIT | Null until scored |
| AnsweredAt | DATETIME2 | Null |
| — | — | UQ (AttemptId, QuestionId) |

**AttemptViolation**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| ViolationId | INT | PK |
| AttemptId | INT | FK → AssessmentAttempt |
| Type | TINYINT | 1 Exit fullscreen, 2 Tab switch, 3 Camera lost, 4 Reload |
| OccurredAt | DATETIME2 | Required |

**SkillValidation**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| ValidationId | INT | PK |
| UserId | INT | FK → User |
| SkillId | INT | FK → Skill |
| AttemptId | INT | FK → AssessmentAttempt, UQ |
| Score | INT | 0–100 |
| ValidationLevelId | INT | FK → ValidationLevel |
| ValidatedAt | DATETIME2 | Required |
| ExpiresAt | DATETIME2 | Required |
| Status | TINYINT | 1 Active, 2 Expired, 3 Replaced |
| — | — | Filtered UQ (UserId, SkillId) where Status = Active |

#### Projects, matching and teams

**Project**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| ProjectId | INT | PK |
| OwnerId | INT | FK → User (Founder) |
| Name | NVARCHAR(100) | Required |
| Category | NVARCHAR(50) | Required |
| PublicSummary | NVARCHAR(500) | Required |
| PrivateDetails | NVARCHAR(4000) | Null; shown only to team members |
| TeamSize | INT | 2–20 |
| Status | TINYINT | 1 Draft, 2 Open, 3 Team Formed, 4 Closed |
| PublishedAt | DATETIME2 | Null |

**ProjectSkillRequirement**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| RequirementId | INT | PK |
| ProjectId | INT | FK → Project |
| SkillId | INT | FK → Skill |
| MinScore | INT | 0–100 |
| MinExperience | TINYINT | 1–3 |
| RequiredAvailability | TINYINT | Default 1 (Available) |
| Openings | INT | At least 1 |
| FilledCount | INT | Default 0; never greater than Openings |

**Application**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| ApplicationId | INT | PK |
| RequirementId | INT | FK → ProjectSkillRequirement |
| TalentId | INT | FK → User |
| Message | NVARCHAR(500) | Null |
| Status | TINYINT | 1 Pending, 2 Accepted, 3 Rejected, 4 Withdrawn, 5 Cancelled |
| DecidedAt | DATETIME2 | Null |
| DecisionReason | NVARCHAR(300) | Null |
| — | — | Filtered UQ (RequirementId, TalentId) where Status = Pending |

**Invitation**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| InvitationId | INT | PK |
| RequirementId | INT | FK → ProjectSkillRequirement |
| TalentId | INT | FK → User |
| FounderId | INT | FK → User |
| Message | NVARCHAR(500) | Null |
| Status | TINYINT | 1 Pending, 2 Accepted, 3 Declined, 4 Expired, 5 Cancelled |
| ExpiresAt | DATETIME2 | Default created date + 7 days |
| RespondedAt | DATETIME2 | Null |
| — | — | Filtered UQ (RequirementId, TalentId) where Status = Pending |

**Team**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| TeamId | INT | PK |
| ProjectId | INT | FK → Project, UQ |
| FormedBy | INT | FK → User (Founder) |

**TeamMember**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| TeamMemberId | INT | PK |
| TeamId | INT | FK → Team |
| UserId | INT | FK → User |
| RequirementId | INT | FK → ProjectSkillRequirement, null for the Founder |
| Position | NVARCHAR(100) | Required |
| Source | TINYINT | 1 Founder, 2 Application, 3 Invitation |
| JoinedAt | DATETIME2 | Required |
| LeftAt | DATETIME2 | Null |
| — | — | UQ (TeamId, UserId) |

#### Platform and chat

**Notification**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| NotificationId | INT | PK |
| UserId | INT | FK → User |
| Type | TINYINT | Application, Invitation, Team, Validation, System |
| Title / Body | NVARCHAR(100) / NVARCHAR(500) | Required |
| RelatedEntityType / RelatedEntityId | NVARCHAR(50) / INT | Null; link to the related record |
| IsRead | BIT | Default 0 |

**AuditLog**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| AuditLogId | BIGINT | PK |
| UserId | INT | FK → User, null for system actions |
| Action | NVARCHAR(100) | Required |
| EntityType / EntityId | NVARCHAR(50) / INT | Null |
| Details | NVARCHAR(2000) | Null |
| IpAddress | NVARCHAR(45) | Null |

**SystemSetting**

| Attribute | Type | Key / Rule |
| --- | --- | --- |
| SettingKey | NVARCHAR(100) | PK; for example Match.Weight.Skills |
| Value | NVARCHAR(500) | Required |
| UpdatedBy | INT | FK → User (Admin) |
| UpdatedAt | DATETIME2 | Required |

**Conversation**, **ConversationMember**, **Message** (optional, FR-035)

| Table | Attributes |
| --- | --- |
| Conversation | ConversationId (PK), TeamId (FK → Team, UQ), CreatedAt |
| ConversationMember | ConversationId (PK part, FK → Conversation), UserId (PK part, FK → User), JoinedAt |
| Message | MessageId (BIGINT, PK), ConversationId (FK → Conversation), SenderId (FK → User), Text (NVARCHAR(1000)), SentAt |

### 7.3 Relationships

| Parent | Child | Type | Meaning |
| --- | --- | --- | --- |
| Role | User | 1 : N | A role has many users; each user has one role |
| User | Profile | 1 : 1 | Each user has one profile |
| User | Availability | 1 : 1 | Each Talent has one availability record |
| User | RefreshToken / EmailVerificationToken | 1 : N | A user can have many tokens over time |
| User and Skill | UserSkill | N : M | A Talent selects many skills; a skill is chosen by many Talents |
| Skill | Assessment | 1 : N | A skill has assessment rules (one active at a time) |
| Assessment | ValidationLevel | 1 : N | Each assessment defines its own score bands |
| Skill | Question | 1 : N | A skill has many questions |
| Question | QuestionOption | 1 : N | A question has 2–6 options, one correct |
| Assessment and Question | AssessmentQuestion | N : M | An assessment draws from many questions; a question can serve several assessments |
| User | AssessmentAttempt | 1 : N | A Talent can make many attempts |
| Assessment | AssessmentAttempt | 1 : N | An assessment is attempted many times |
| AssessmentAttempt | AssessmentAnswer | 1 : N | An attempt holds one answer row per question |
| Question / QuestionOption | AssessmentAnswer | 1 : N each | An answer points to a question and the selected option |
| AssessmentAttempt | AttemptViolation | 1 : N | An attempt can log many violations |
| AssessmentAttempt | SkillValidation | 1 : 0..1 | Only a passed (or approved) attempt creates a validation |
| User and Skill | SkillValidation | 1 : N | A Talent has many validations over time; only one is Active per skill |
| ValidationLevel | SkillValidation | 1 : N | Each validation has one level |
| User (Founder) | Project | 1 : N | A Founder owns many projects |
| Project | ProjectSkillRequirement | 1 : N | A project has many positions |
| Skill | ProjectSkillRequirement | 1 : N | A requirement uses one skill |
| ProjectSkillRequirement | Application / Invitation | 1 : N | A position receives many applications and invitations |
| User (Talent) | Application / Invitation | 1 : N | A Talent sends many applications and receives many invitations |
| User (Founder) | Invitation | 1 : N | A Founder sends many invitations |
| Project | Team | 1 : 0..1 | A project has at most one team |
| Team | TeamMember | 1 : N | A team has many members |
| User | TeamMember | 1 : N | A user can be in many teams over time; the Talent availability rule limits active teams to one |
| ProjectSkillRequirement | TeamMember | 1 : N | A member fills one position (null for the Founder) |
| Team | Conversation | 1 : 0..1 | A team has at most one chat |
| Conversation | ConversationMember / Message | 1 : N | A chat has many members and messages |
| User | Notification / AuditLog / Message | 1 : N | A user owns many notifications, audit records and messages |

### 7.4 Integrity Rules and Indexes

- Foreign keys use `ON DELETE NO ACTION`. Records are deactivated (`IsActive = 0`) instead of deleted, except tokens and notifications.
- Create indexes on: `User(Email)`, `UserSkill(UserId, SkillId)`, `SkillValidation(SkillId, Status, Score)`, `Availability(Status)`, `Project(Status)`, `ProjectSkillRequirement(ProjectId)`, `Application(RequirementId, Status)`, `Invitation(TalentId, Status)`, `Notification(UserId, IsRead)`, `AuditLog(CreatedAt)`.
- Status values are stored as small numbers and shown as text by the application; the meaning of each number is listed above.
- Team formation (FR-030) must run inside one database transaction.


## 8. UI/UX Requirements

The interface must make trust visible: validation scores, levels, expiry dates and availability are always shown next to a person's name.

### 8.1 Main Pages

| Page | Role | Purpose and key elements |
| --- | --- | --- |
| Landing | Guest | Value proposition (Validate → Trust → Match → Team), how it works, Register and Login buttons |
| Register / Login / Verify Email | Guest | Forms with field errors; Google button; role choice on register |
| Onboarding | Talent, Founder | Step form: profile, picture, experience level, skills (Talent) |
| Talent Dashboard | Talent | Availability switch, skill cards with status, open invitations, application status, suggested projects |
| My Profile / My Skills | Talent | Verified profile preview; skill list with Validate and Renew buttons and expiry dates |
| Assessment Instructions | Talent | Rules, time, attempts left, monitoring notice, disclaimer, system check, Start button |
| Assessment Room | Talent | Fullscreen exam: timer, question navigator, one question at a time, warning banner for violations |
| Assessment Result | Talent | Score, level, expiry date, retake date if failed, disclaimer about real-world expertise |
| Browse Projects / Project Details | Talent | Filters, project cards with match score, requirements, Apply button |
| My Applications / My Invitations | Talent | Tabs by status; Accept and Decline buttons on invitations |
| Founder Dashboard | Founder | Project cards with status, pending applications count, quick actions |
| Create / Edit Project and Requirements | Founder | Project form plus a requirements table (add, edit, remove rows) |
| Recommended Talents | Founder | Ranked talent cards per requirement with match score, breakdown and Invite button |
| Talent Search / Talent Profile View / Compare | Founder | Filters; profile with validated skills; side-by-side table for 2–4 talents |
| Applications Review / Sent Invitations | Founder | Lists with Accept and Reject; invitation status |
| Team Page | Founder, Talent | Members, positions, private project details, optional chat |
| Notifications | All signed in | List with unread badge in the top bar |
| Admin Dashboard | Admin | Analytics cards and charts |
| Users, Skills, Question Bank, Assessment Rules, Attempt Review, Projects Monitor, Audit Logs, Platform Settings | Admin | Data tables with search, filters, paging and edit forms |

### 8.2 Navigation Flow

**Talent:** Landing → Register → Verify Email → Onboarding → My Skills → Assessment Instructions → Assessment Room → Assessment Result → My Profile → set availability → Browse Projects → Project Details → Apply → My Applications → Team Page. Invitations arrive in My Invitations and in Notifications and lead to Team Page when accepted.

**Founder:** Landing → Register → Verify Email → Onboarding → Create Project → Requirements → Publish → Recommended Talents → Talent Profile View (or Search and Compare) → Invite → Applications Review → Confirm Team → Team Page.

**Admin:** Login → Admin Dashboard → Skills → Question Bank → Assessment Rules → Platform Settings; Attempt Review, Users, Projects Monitor and Audit Logs from the side menu.

Navigation rules:

- A signed-in user sees a top bar (logo, notifications, profile menu) and a side menu (desktop) or bottom bar (mobile) with only the pages of their role.
- Opening a page of another role shows a 403 page with a link back to the dashboard.
- During an assessment the normal navigation is hidden; leaving the page counts as a violation.
- Every destructive or final action (Reject, Decline, Confirm Team, Block user, Close project) shows a confirmation dialog.

### 8.3 Responsive Design Requirements

| Breakpoint | Width | Layout |
| --- | --- | --- |
| Mobile | under 640 px | One column; bottom navigation; filters in a slide-up panel; tables become cards |
| Tablet | 640–1023 px | Two columns for cards; collapsible side menu |
| Desktop | 1024 px and above | Side menu, up to 3–4 columns for cards, full tables |

- Design mobile first with Tailwind CSS breakpoints.
- No horizontal page scrolling from 320 px width.
- Touch targets are at least 44 × 44 px.
- Assessments can be taken on desktop and laptop; on a phone the Assessment Instructions page shows a notice if fullscreen or camera is unavailable.
- Compare Candidates shows a horizontally scrollable table on small screens with the first column fixed.

### 8.4 Color and Design Guidelines

| Token | Color | Use |
| --- | --- | --- |
| Primary | `#1D4ED8` (blue) | Main buttons, links, active menu item |
| Secondary | `#0F766E` (teal) | Validated badges, Advanced level, success highlights |
| Accent | `#F59E0B` (amber) | Highlights and badges (use dark text on it) |
| Success | `#15803D` | Accepted, Available |
| Warning | `#B45309` | Pending, Expiring soon |
| Danger | `#B91C1C` | Rejected, Expired, errors, violations |
| Text | `#111827` / `#4B5563` | Main text / secondary text |
| Background / Surface / Border | `#F9FAFB` / `#FFFFFF` / `#E5E7EB` | Page, cards, dividers |

Guidelines:

- **Trust badges:** a validation shows as `React.js 91% Validated` with a level label (Basic, Intermediate, Advanced) and an "Expires" date. Expired skills are grayed out with the word Expired.
- **Status chips:** always icon plus text, never color only (see NFR-026).
- **Typography:** Inter (or system font stack); body 16 px; headings 24, 20 and 18 px; line height 1.5.
- **Shape and spacing:** 8 px spacing grid; cards with 12 px radius and light shadow; one primary button per screen section.
- **Match score:** shown as a number with a labeled bar (Strong, Good, Partial) and a "How is this calculated?" link that opens the factor breakdown.
- **Disclaimers:** the sentence "The assessment does not guarantee real-world expertise. It provides a standardized validation signal." appears on the result page and on talent profiles.
- **Feedback:** every action shows a toast (success or error); every list has loading, empty and error states; forms validate on blur and on submit.
- **Language:** English first; layout must allow adding Arabic (right-to-left) later by using logical CSS properties.

## 9. Business Rules

These rules apply everywhere in the system. Values marked "default" are configurable by the Admin.

### 9.1 Accounts, Assessments and Validation

| ID | Rule | Related |
| --- | --- | --- |
| BR-01 | One account has exactly one role. Admin accounts are created only by an existing Admin or by the initial database seed, never by public registration. | FR-001, FR-005 |
| BR-02 | Email is unique. A user with an unverified email cannot take assessments, apply or send invitations. | FR-004 |
| BR-03 | A blocked user cannot log in. Their Pending applications and invitations become Cancelled. | FR-032 |
| BR-04 | A Talent can only take an assessment for a skill they have added, and only if the skill has enough active questions. | FR-009, FR-012 |
| BR-05 | Attempts per skill are limited (default 3 attempts in any 30 days) with a wait between attempts (default 24 hours). Only one attempt can be In Progress at a time. | FR-011, FR-012 |
| BR-06 | Score = correct answers ÷ total questions × 100, rounded. The default pass score is 60. Default levels: 60–69 Basic, 70–84 Intermediate, 85–100 Advanced. | FR-015 |
| BR-07 | A validation is valid for a set period (default 12 months). Expired validations are not used in matching, search score filters or applications. A newer passed assessment replaces the old validation. | FR-015, FR-016 |
| BR-08 | Reaching the violation limit (default 3) submits the attempt automatically and flags it. A flagged attempt creates no validation until an Admin approves it. | FR-014 |
| BR-09 | The system and its texts must never claim that cheating is fully prevented or that a score guarantees real-world expertise. The disclaimer must be shown on assessment and result pages and on talent profiles. | FR-012, FR-015 |

### 9.2 Availability

| ID | Rule | Related |
| --- | --- | --- |
| BR-10 | Availability has three states: Available, Currently in a Team, Not Available. Only Available talents can receive invitations, apply, or have an application accepted. | FR-017 |
| BR-11 | When a Talent joins a team, availability changes automatically to Currently in a Team. A Talent in a team belongs to one active team at a time and can only change status after leaving the team or by Admin action. | FR-017, FR-030 |

### 9.3 Matching

| ID | Rule | Related |
| --- | --- | --- |
| BR-12 | Each factor is a value from 0 to 100, calculated per Talent and per position. **Skills** = required skills the Talent holds with an Active validation ÷ number of required skills × 100. **Validation** = average over the required skills of the smaller of 100 and (score ÷ minimum score × 100); a missing skill counts as 0. **Experience** = 100 if the Talent's level is at or above the required level, 50 if one level below, otherwise 0. **Availability** = 100 if Available, otherwise 0. The final score is rounded to a whole number. | FR-022 |
| BR-13 | Match weights default to Skills 40, Validation 30, Experience 20, Availability 10. They are stored as settings, must add up to 100, and are never hard-coded. Every change is written to the audit log. | FR-022 |
| BR-14 | Labels: Strong Match = score 80–100 and every minimum is met; Good Match = 60–79 (also the highest label for a talent who does not meet every minimum, marked "Below minimum"); Partial Match = 40–59; below 40 is not recommended. | FR-021 |
| BR-15 | Recommendations list only Available talents with a verified email. Talent Search shows all talents but filters to Available by default. | FR-021, FR-023 |
| BR-16 | Foundly recommends, the Founder decides. A match score never accepts, rejects or invites anyone automatically. | FR-021 |

### 9.4 Projects, Applications, Invitations and Teams

| ID | Rule | Related |
| --- | --- | --- |
| BR-17 | A project can be published (Draft → Open) only with at least one position, and each position has at least one skill. Only the owner edits or closes a project. A position with accepted members cannot be removed. | FR-018, FR-019 |
| BR-18 | Private project details are visible only to the owner and team members. Everyone else sees the public summary and the requirements. | FR-020 |
| BR-19 | The Founder counts as a team member. The total openings of a project cannot exceed team size minus one. | FR-019 |
| BR-20 | A Talent can apply only if Available, verified by email, and meeting every skill minimum of the position. One Pending application per position; no applications to own or closed projects. | FR-026 |
| BR-21 | An invitation goes only to an Available Talent. It expires after 7 days (default). One Pending invitation per Talent and position; at most 10 open invitations per project. | FR-028 |
| BR-22 | Accepted and Rejected (or Declined) decisions are final. A Talent can withdraw a Pending application; a Founder can cancel a Pending invitation. | FR-027, FR-029 |
| BR-23 | When all openings of a position are filled, remaining Pending applications and invitations for it become Cancelled automatically. | FR-027, FR-029 |
| BR-24 | Confirming a team (in one transaction): creates the team, sets members to Currently in a Team, cancels their other Pending requests, sets the project to Team Formed and notifies members. | FR-030 |

### 9.5 Platform and Scope

| ID | Rule | Related |
| --- | --- | --- |
| BR-25 | Foundly stops at team formation. Tasks, files, meetings, funding and project management are not built. Any new feature must support Validate, Trust, Match or Team. | All |
| BR-26 | Profiles show only name, picture, bio, main role, experience, validated skills, availability and expiry dates. No phone number, address or full work history is stored. | FR-006 |
| BR-27 | Audit records cannot be edited or deleted through the application. Business records are deactivated, not deleted; a skill with linked data cannot be deleted. | FR-008, FR-034 |
| BR-28 | Premium plans, B2B portals and payments are outside the MVP. | Section 12 |
