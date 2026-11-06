# LiftHub — Product Requirements Document

**Version:** 1.0  
**Status:** Draft  
**Platform:** Android  
**Framework:** Flutter  
**Backend:** Supabase  
**Database:** PostgreSQL  

## 1. Product Overview

### 1.1 Description

LiftHub is a Smart Gym Management System designed to help gym managers and trainers manage daily gym operations through a single Android application.

The application provides tools for managing members, memberships, payments, attendance, trainers, workout plans, and fitness progress.

LiftHub uses role-based interfaces to provide different functionality to gym managers and trainers.

Members are maintained as records within the system and do not have individual accounts or application access in V1.

### 1.2 Objectives

The primary objectives of LiftHub are:

- Simplify everyday gym management.
- Centralize member and membership records.
- Track payments and outstanding balances.
- Monitor member attendance.
- Enable trainers to manage assigned members and workout plans.
- Track members' fitness progress.
- Provide managers with useful gym statistics and reports.

### 1.3 Target Users

LiftHub targets individual gyms of different sizes.

Each gym operates independently within the application. Multi-branch management is not supported in V1.

---

## 2. Project Scope

### 2.1 In Scope — V1

The first version will include:

1. Manager and trainer authentication.
2. Role-based application interfaces.
3. Member registration and management.
4. Membership plan creation and management.
5. Membership assignment and expiry management.
6. Manual payment recording and tracking.
7. Attendance recording and monitoring.
8. Trainer profile management.
9. Member-to-trainer assignments.
10. Workout plan creation and management.
11. Fitness progress tracking.
12. Gym dashboard and statistics.
13. Basic reports.
14. In-app notifications.

### 2.2 Out of Scope — V1

The following features are explicitly excluded:

- Individual member accounts or member-facing applications.
- Social features and community.
- AI-generated workout plans.
- Nutrition and meal tracking.
- Sleep and water tracking.
- Wearable integrations.
- Multi-branch management.
- Advanced business intelligence.
- Online payment gateway integration.
- Progress photos.
- Offline synchronization.
- Report and data exports.
- Push notifications.

These exclusions must be respected throughout development.

---

## 3. User Roles and Permissions

LiftHub will use a single application with role-based interfaces.

### 3.1 Gym Manager

Each gym will have one manager account in V1.

The manager has administrative control over the gym and can:

- View the gym dashboard and statistics.
- Register, view, update, and manage members.
- Create and manage membership plans.
- Assign memberships to members.
- Monitor membership expiry.
- Record and manage payments.
- View outstanding balances.
- Record and monitor attendance.
- Add and manage trainer profiles.
- Assign members to trainers.
- View gym statistics and basic reports.
- Review and approve trainer registrations.

### 3.2 Trainer

Trainers have restricted access based on their assigned responsibilities.

A trainer can:

- View their assigned members.
- Access relevant information about assigned members.
- Create and manage workout plans for assigned members.
- Monitor members' fitness progress.
- Record and monitor attendance for assigned members.

Trainers cannot access administrative functionality such as membership plan management, payment management, or overall gym administration.

### 3.3 Gym Members

Members do not have application accounts.

Their records are managed by the gym manager and accessed by trainers according to their assignments.

Member records contain basic personal and registration information, alongside their membership, payment, attendance, and fitness-related records.

---

## 4. Authentication and Account Management

### 4.1 Authentication

Supabase Authentication will handle user authentication.

The application will support two account roles:

- Gym Manager
- Trainer

Users must authenticate before accessing the application.

### 4.2 Manager Account

The gym manager account will be created during initial gym registration or controlled first-time setup.

Each gym supports exactly one manager account in V1. The initial manager must complete the gym setup before normal operations can begin.

### 4.3 Trainer Registration and Onboarding

Trainers can register themselves through the application.

New trainers must complete the onboarding profile during registration and remain pending until approved by the gym manager. Pending trainers cannot access trainer functionality or assigned member data. Approved trainers receive access only after manager approval. A rejected registration does not grant access and must not create a usable trainer account for the same onboarding flow.

### 4.4 Role-Based Access

After authentication, users will be directed to the appropriate interface according to their assigned role.

Access to application features and data must be enforced through backend authorization and Supabase Row Level Security (RLS), not merely by hiding interface elements.


# 5. Functional Requirements

This section defines the expected functionality and behavior of LiftHub V1.

## 5.1 Member Management

The system shall allow the gym manager to manage gym members.

### 5.1.1 Member Registration

The manager shall be able to register new members by providing basic information.

The initial member information shall include:

- Full name.
- Phone number.
- Registration date (automatically recorded).

Additional member information may be maintained where necessary, but V1 should avoid unnecessarily complicated member profiles.

### 5.1.2 Member Operations

The manager shall be able to:

- View all registered members.
- Search members by name or phone number.
- View individual member profiles.
- Update member information.
- View membership details.
- View payment history.
- View attendance history.
- View assigned trainer.
- View fitness progress records.

### 5.1.3 Member Status

The system shall maintain the operational status of members.

A member may have the following statuses:

- Active.
- Inactive.

Membership expiry and member status must be treated separately. An expired membership does not automatically delete or deactivate the member's record.

### 5.1.4 Member Record Retention

Member records must remain available after membership expiry.

Historical information, including payments, attendance, membership assignments, and fitness progress, must be preserved.

Deleting or deactivating a member must not unintentionally delete their historical records.

---

## 5.2 Membership Management

The system shall allow the manager to create and manage membership plans and assign them to members.

### 5.2.1 Membership Plan Creation

The manager shall be able to create customizable membership plans.

Each plan shall contain:

- Plan name.
- Duration.
- Price.
- Description (optional).
- Status (active or inactive).

The system shall support different durations, such as monthly, quarterly, and yearly memberships.

The manager may create plans according to the gym's requirements.

### 5.2.2 Membership Plan Management

The manager shall be able to:

- View all membership plans.
- Create new plans.
- Update existing plans.
- Activate or deactivate plans.

Deactivating a plan must not affect existing membership assignments or their historical records.

### 5.2.3 Membership Assignment

The manager shall be able to assign a membership plan to a registered member.

An assignment shall record:

- Member.
- Selected membership plan.
- Start date.
- Expiry date.
- Membership price at the time of assignment.
- Membership status.

The system shall calculate the expiry date using the selected plan's duration.

### 5.2.4 Membership Renewal

The manager shall be able to renew an existing membership.

If a member renews before the current membership expires, the new membership shall begin immediately after the existing membership's expiry.

If the existing membership has already expired, the new membership shall begin on the new assignment date.

The system must preserve previous membership assignments as historical records.

### 5.2.5 Membership Status

Memberships shall have the following statuses:

- Active.
- Expired.

The system shall determine membership expiry using the recorded expiry date and the expiry is inclusive. A membership remains valid through its recorded expiry date and becomes expired only after that date has ended. For example, a membership expiring on 30 June remains valid through 30 June, and the member is treated as expired starting 1 July.

Expired memberships must remain accessible in the member's history.

### 5.2.6 Membership Expiry Monitoring

The manager shall be able to:

- View active memberships.
- View expired memberships.
- Identify memberships approaching expiry.
- View members whose memberships have expired.

The dashboard shall highlight memberships expiring soon. Expiry monitoring must treat the recorded expiry date as the final valid day of the membership and must not exclude the expiry date from active membership visibility.

The expiry monitoring functionality must not depend on push notifications.

---

## 5.3 Payment Management

The system shall allow the manager to record and monitor member payments.

All payments in V1 will be recorded manually. No online payment gateway will be integrated.

### 5.3.1 Payment Recording

The manager shall be able to record payments against a member's membership.

Each payment shall contain:

- Member.
- Associated membership assignment.
- Payment amount.
- Payment date.
- Payment method.
- Optional notes.

Supported payment methods may include:

- Cash.
- Bank transfer.
- Other.

### 5.3.2 Full and Partial Payments

The system shall support both full and partial payments.

A member may make multiple payments toward a single membership assignment.

The system shall calculate:

**Outstanding Balance = Membership Amount − Total Payments Received**

The system shall maintain an accurate record of the total amount paid and the remaining balance.

### 5.3.3 Payment Management

The manager shall be able to:

- View all payments.
- View payments associated with a member.
- View payment history for a membership.
- Record additional payments.
- Correct or manage existing payment records.

Payment modifications must update the associated outstanding balance accordingly.

Historical payment information must remain traceable.

### 5.3.4 Outstanding Payments

The system shall allow the manager to identify members with outstanding balances.

The manager shall be able to view:

- Total membership amount.
- Amount paid.
- Outstanding balance.

### 5.3.5 Payment Restrictions

Trainers shall not have access to payment management functionality.

Only the manager can record or modify payments.

---

## 5.4 Attendance Management

The system shall provide manual attendance recording and monitoring.

### 5.4.1 Attendance Recording

The manager shall be able to:

- Search for a registered member.
- View the member's current membership status.
- Mark the member as present.
- View attendance records.

Trainers shall also be able to record and monitor attendance for their assigned members.

### 5.4.2 Duplicate Prevention

The system must prevent a member from receiving multiple attendance entries for the same gym date.

Before recording attendance, the application must check whether an attendance record already exists for that member on the current date.

Duplicate prevention must also be enforced at the database level to prevent simultaneous requests or repeated submissions from creating duplicate records.

### 5.4.3 Attendance Records

Each attendance record shall contain:

- Member.
- Attendance date.
- Check-in time.
- Recorded by (manager or trainer).

### 5.4.4 Attendance History

The manager shall be able to:

- View overall attendance.
- View attendance for an individual member.
- Filter attendance by date.
- Monitor daily attendance.

Trainers shall only access attendance information relevant to their assigned members.

### 5.4.5 Membership Restrictions

Members with expired memberships should not be allowed to receive normal attendance entries.

The system should validate membership status before recording attendance.

A manager may create an attendance override for an exceptional administrative correction, but the override must be clearly marked as a correction, must not create a duplicate attendance record for the same member and gym date, and must not be used as a routine bypass of ordinary membership validation. Trainers shall not be able to override attendance status for members.

---

## 5.5 Trainer Management

The system shall allow the manager to manage trainer records and assignments.

### 5.5.1 Trainer Registration

Trainers shall be able to register through the application.

New registrations shall remain pending until approved by the manager.

### 5.5.2 Trainer Approval

The manager shall be able to:

- View pending trainer registrations.
- Approve trainer registrations.
- Reject trainer registrations.
- View approved trainers.

Only approved trainers may access trainer functionality.

### 5.5.3 Trainer Profiles

Trainer profiles shall contain relevant information, including:

- Full name.
- Phone number.
- Email address.
- Specialization (optional).
- Account status.

### 5.5.4 Trainer Management

The manager shall be able to:

- View all trainers.
- View individual trainer profiles.
- Update trainer information.
- Activate or deactivate trainers.
- Maintain historical trainer records when a trainer is deactivated.

Deactivating a trainer shall prevent the trainer from receiving new member assignments and from accessing trainer functionality, but shall not delete historical records, member assignments, or trainer account history. A deactivated trainer may be reactivated later without losing historical data. A trainer who is deactivated must not be assigned new members until reactivated.

### 5.5.5 Member Assignment

The manager shall be able to assign members to trainers.

The manager shall also be able to:

- View members assigned to a trainer.
- Change a member's assigned trainer.
- Remove a trainer assignment.
- Reassign a member from a deactivated trainer to an active trainer.

A trainer shall only access members assigned to them.

Changing a member's assigned trainer must not delete the member's existing workout plans, fitness progress, or attendance history. Deactivating or changing a trainer must not remove the member's historical records or invalidate past attendance, payment, or progress information.

---

## 5.6 Workout Plan Management

The system shall allow trainers to create and manage workout plans for their assigned members.

### 5.6.1 Workout Plan Creation

A trainer shall be able to create a workout plan for an assigned member.

Each workout plan shall contain:

- Plan name.
- Assigned member.
- Creating trainer.
- Start date.
- End date (optional).
- Workout days.
- Exercises for each workout day.
- Sets.
- Repetitions.
- Weight (optional).
- Instructions or notes (optional).

### 5.6.2 Workout Structure

A workout plan shall contain multiple workout days.

Each workout day shall contain one or more exercises.

Each exercise shall maintain its relevant training information, including sets, repetitions, optional weight, and instructions.

### 5.6.3 Plan Management

Trainers shall be able to:

- Create workout plans.
- View their assigned members' workout plans.
- Update existing plans.
- Manage exercises within plans.

### 5.6.4 Plan Limitation

V1 shall maintain one current workout plan per member.

A trainer may update the existing plan when the member's training routine changes.

The system should retain the relevant plan information rather than unnecessarily creating multiple simultaneously active plans for the same member.

### 5.6.5 Access Restrictions

Trainers may manage workout plans only for their assigned members.

The manager may view workout plan information for administrative oversight.

---

## 5.7 Fitness Progress Tracking

The system shall allow trainers to record and monitor the fitness progress of their assigned members.

### 5.7.1 Progress Records

Trainers shall be able to record:

- Body weight.
- Body measurements.
- Progress notes.

Body measurements may include:

- Chest.
- Waist.
- Arms.
- Thighs.
- Other relevant measurements.

Measurements should be optional so trainers can record only the information relevant to a member.

### 5.7.2 Progress History

Each progress record shall contain:

- Member.
- Recording date.
- Recorded measurements.
- Weight.
- Notes.
- Recording trainer.

### 5.7.3 Progress Monitoring

Trainers shall be able to:

- Add new progress records.
- View previous records.
- Update relevant progress information.
- Compare historical measurements.

The application should provide a simple visual representation of progress over time where sufficient records exist.

### 5.7.4 Access Restrictions

Trainers may manage progress records for their assigned members.

The manager may view fitness progress for administrative oversight.

Progress photographs and AI-based progress analysis are excluded from V1.

---

## 5.8 Manager Dashboard

The manager dashboard shall provide an overview of the gym's current operational status.

### 5.8.1 Dashboard Statistics

The dashboard shall display:

| Statistic | Description |
|---|---|
| Total Members | Total registered members |
| Active Members | Members currently marked active |
| Expired Memberships | Memberships that have expired |
| Expiring Soon | Memberships approaching expiry |
| Today's Attendance | Number of unique members marked present today |
| Total Trainers | Number of approved active trainers |
| Monthly Revenue | Payments received during the current month |
| Pending Payments | Outstanding membership balances |

### 5.8.2 Dashboard Navigation

The dashboard shall provide convenient navigation to the relevant management sections.

### 5.8.3 Data Accuracy

Dashboard statistics must reflect the latest available database records.

Financial statistics shall be calculated using recorded payments rather than assigned membership prices.

---

## 5.9 Reports

The system shall provide basic reports to help the manager monitor gym operations.

### 5.9.1 Membership Report

The membership report shall provide information about:

- Active memberships.
- Expired memberships.
- Memberships approaching expiry.
- Membership assignments.

### 5.9.2 Attendance Report

The attendance report shall provide:

- Daily attendance.
- Attendance history.
- Member-specific attendance.
- Date-based attendance filtering.

### 5.9.3 Payment and Revenue Report

The payment report shall provide:

- Payments received.
- Payment history.
- Outstanding balances.
- Revenue over a selected period.

### 5.9.4 Member Registration Report

The member registration report shall provide:

- Registered members.
- Registration dates.
- Date-based registration filtering.

### 5.9.5 Report Restrictions

Reports shall be viewable inside the application.

PDF, CSV, Excel, and other export functionality are excluded from V1.

---

## 5.10 In-App Notifications

The application shall provide an in-app notification center for relevant gym management updates.

### 5.10.1 Notification Types

V1 shall support notifications related to:

- Memberships approaching expiry.
- Expired memberships.
- Outstanding payments.
- Pending trainer registrations.

Notification delivery shall be role-specific. The manager shall receive gym-wide operational notifications, such as pending trainer registrations, memberships approaching expiry or expired, and outstanding payment alerts. Trainers shall receive only notifications relevant to their assigned members and their own trainer account status, and shall not receive manager-only administrative notifications or unrelated financial information.

### 5.10.2 Notification Management

Users shall be able to:

- View available notifications.
- Identify unread notifications.
- Open relevant sections from notifications where applicable.
- Mark notifications as read.

### 5.10.3 Notification Restrictions

Notifications shall be available only inside the application.

Push notifications and external notification delivery are excluded from V1.

Notifications should be generated or updated based on relevant system events and conditions without requiring users to manually create reminders.

---

# 6. Business Rules

This section defines rules that must remain consistent throughout the application.

| ID | Business Rule |
|---|---|
| BR-01 | Each gym supports one manager account in V1. |
| BR-02 | Trainers must be approved by the manager before accessing trainer functionality. |
| BR-03 | Members do not have application accounts. |
| BR-04 | Each member belongs to one gym. |
| BR-05 | An expired membership does not automatically delete or deactivate its member. |
| BR-06 | A member may have historical membership assignments. |
| BR-07 | A member should have no more than one current active membership. |
| BR-08 | Renewals begin after the existing membership expires. |
| BR-09 | New memberships begin on the assignment date when there is no unexpired membership. |
| BR-10 | Membership expiry must be determined using stored membership dates. |
| BR-11 | Membership plans cannot be deleted in a way that damages historical assignments. |
| BR-12 | Membership assignments retain the agreed membership price at the time of assignment. |
| BR-13 | Payments are recorded manually by the manager. |
| BR-14 | Multiple partial payments may be associated with one membership assignment. |
| BR-15 | Outstanding balances are calculated using the assigned membership amount and recorded payments. |
| BR-16 | Payment records must be associated with the appropriate member and membership assignment. |
| BR-17 | A member cannot have duplicate attendance entries for the same gym date. |
| BR-18 | Normal attendance requires a valid active membership. |
| BR-19 | Trainers may access only their assigned members' relevant information. |
| BR-20 | A member may have only one current workout plan in V1. |
| BR-21 | Historical attendance, payment, membership, and progress records must be preserved. |
| BR-22 | Dashboard revenue represents payments received, not merely assigned membership fees. |
| BR-23 | Only the manager can access administrative financial and membership management functionality. |
| BR-24 | Backend authorization must enforce role-based access restrictions. |
| BR-25 | Each gym must complete an initial registration and setup process before manager-led operations can begin. |
| BR-26 | The gym manager account is the single administrative account for the gym in V1. |
| BR-27 | A trainer must complete registration onboarding before the manager can approve the trainer account. |
| BR-28 | Pending trainers cannot access trainer functionality or assigned member records until manager approval is granted. |
| BR-29 | Deactivating a trainer removes future access and new assignments but preserves historical records and prior trainer relationships. |
| BR-30 | A deactivated trainer cannot be assigned new members until reactivated. |
| BR-31 | Changing a member's assigned trainer does not delete that member's historical workout, progress, or attendance records. |
| BR-32 | Attendance overrides are manager-only and must be clearly marked as an administrative correction. |
| BR-33 | Attendance overrides do not create duplicate attendance records and must not bypass ordinary membership validation for routine usage. |
| BR-34 | Membership expiry is inclusive; a membership remains valid through its recorded expiry date and expires after that date ends. |
| BR-35 | Notifications are role-scoped so managers receive gym-level operational notifications and trainers receive only notifications relevant to their assigned members and trainer account. |

---

# 7. Data Requirements

This section identifies the main information categories that LiftHub must maintain. It does not define the final database schema.

## 7.1 Main Data Entities

The application will require the following logical entities:

| Entity | Purpose |
|---|---|
| Gym | Represents the gym using LiftHub |
| User | Stores authenticated manager and trainer account information |
| Member | Stores gym member records |
| Membership Plan | Stores available membership plans |
| Membership | Stores individual membership assignments and their history |
| Payment | Stores payments associated with membership assignments |
| Attendance | Stores member attendance records |
| Trainer Assignment | Represents the relationship between members and trainers |
| Workout Plan | Stores a member's current workout plan |
| Workout Day | Represents individual days within a workout plan |
| Exercise | Stores exercises belonging to workout days |
| Progress Record | Stores historical fitness measurements and notes |
| Notification | Stores in-app notifications |

## 7.2 Data Relationships

The logical relationships shall follow these principles:

- One gym has one manager in V1.
- One gym can have multiple trainers.
- One gym can have multiple members.
- One member can have multiple historical membership assignments.
- One membership plan can be used by multiple membership assignments.
- One membership assignment can have multiple payments.
- One member can have multiple attendance records.
- One trainer can be assigned multiple members.
- A member can have one current assigned trainer.
- One member can have one current workout plan.
- One workout plan can contain multiple workout days.
- One workout day can contain multiple exercises.
- One member can have multiple historical progress records.

## 7.3 Data Integrity

The system shall maintain data consistency through appropriate database constraints and backend validation.

Important considerations include:

- Preventing duplicate attendance.
- Maintaining valid relationships between records.
- Preventing unauthorized access to another gym's data.
- Preventing trainers from accessing unassigned members.
- Preserving historical membership and payment information.
- Maintaining accurate payment balances.
- Preventing invalid membership assignments.

## 7.4 Historical Data

Historical records must remain accessible even when related records become inactive.

For example:

- Deactivating a trainer must not delete their historical records.
- Deactivating a membership plan must not affect existing memberships.
- Changing a member's trainer must not remove previous workout or progress records.
- Expired memberships must remain available for historical reference.

---

# 8. Non-Functional Requirements

## 8.1 Security

- Supabase Authentication shall handle authentication.
- PostgreSQL Row Level Security shall enforce data access restrictions.
- Users must only access functionality and information permitted by their roles.
- Trainers must not access administrative financial information.
- Sensitive operations must be validated on the backend.
- Supabase service-role credentials must never be exposed in the Flutter application.

## 8.2 Performance

- Common application operations should respond promptly under normal network conditions.
- Lists should support appropriate pagination or incremental loading as data grows.
- Dashboard statistics should be retrieved efficiently.
- Database queries should avoid unnecessary data retrieval.

## 8.3 Reliability and Data Integrity

- Important operations must not create duplicate or inconsistent records.
- Failed operations should provide understandable feedback.
- Payment and membership records must remain consistent.
- Critical database operations should use appropriate transactions or atomic operations.
- Data must remain persistent across application restarts.

## 8.4 Connectivity

LiftHub V1 requires an active internet connection.

Offline functionality and synchronization are not required.

The application should provide suitable feedback when network connectivity is unavailable.

## 8.5 Maintainability

- The Flutter application should use a modular and maintainable architecture.
- Business logic should be separated from UI components.
- State management should be consistent throughout the application.
- Database operations should be organized into appropriate service or repository layers.
- Reusable UI components should be used where appropriate.

## 8.6 User Interface

- The application shall follow Material 3 design principles.
- The interface shall be modern, clean, and easy to navigate.
- Manager and trainer interfaces shall expose only their relevant functionality.
- Loading, empty, success, and error states should be handled appropriately.
- Forms should provide input validation and understandable error messages.

## 8.7 Platform

The first release shall target Android devices.

The application shall be developed using Flutter and Dart.

---

# 9. Acceptance Criteria

LiftHub V1 shall be considered functionally complete when the following conditions are satisfied.

### 9.1 Authentication and Authorization

- The gym can be registered and the initial manager account can be created through the controlled setup flow.
- Trainers can register and complete onboarding while awaiting approval.
- The manager can approve or reject trainer registrations.
- Unapproved trainers cannot access trainer functionality or assigned member data.
- Users cannot access unauthorized features or data.

### 9.2 Member Management

- The manager can register, view, search, and update members.
- Member information remains available after membership expiry.
- Historical records are preserved.

### 9.3 Membership Management

- The manager can create and manage membership plans.
- Memberships can be assigned to members.
- Membership expiry is calculated correctly and is inclusive of the recorded expiry date.
- Renewals follow the defined date rules.
- Expired memberships are identifiable.

### 9.4 Payments

- The manager can record full and partial payments.
- Outstanding balances are calculated correctly.
- Payment history is accessible.
- Financial information is restricted to the manager.

### 9.5 Attendance

- The manager and authorized trainers can record attendance.
- Duplicate attendance for the same member and gym date is prevented.
- Attendance history can be viewed and filtered.
- Membership restrictions are enforced.
- Attendance overrides are manager-only, clearly marked, and do not create duplicate attendance entries.

### 9.6 Trainer Management

- The manager can manage trainer profiles.
- Members can be assigned and reassigned to trainers.
- Trainers can only access their assigned members.
- Deactivated trainers cannot receive new assignments and historical records remain available.

### 9.7 Workout Plans

- Trainers can create and update workout plans.
- Plans support workout days and exercises.
- The one-current-plan-per-member restriction is maintained.

### 9.8 Fitness Progress

- Trainers can record weight, measurements, and notes.
- Historical progress records are accessible.
- Progress can be monitored over time.

### 9.9 Dashboard and Reports

- Dashboard statistics display accurate information.
- Revenue reflects actual recorded payments.
- Reports display the relevant information.
- Date-based filtering works where applicable.
- No export functionality is required.

### 9.10 Notifications

- Relevant in-app notifications are available.
- Notifications are routed by role and scope.
- Managers receive gym-level operational notifications and trainers receive only notifications relevant to their assigned members.
- Read and unread states are maintained.
- Push notifications are not required.

---

# 10. V1 Scope Protection

The following rules apply throughout LiftHub development:

1. The finalized V1 scope is the source of truth.
2. Features explicitly excluded from V1 must not be introduced without approval.
3. Copilot must not independently expand product functionality.
4. New requirements must be discussed and approved before implementation.
5. Implementation decisions must remain consistent with the PRD.
6. Technical complexity should be minimized where it does not compromise functionality, security, or data integrity.

The priority is to deliver a complete, functional, and maintainable V1 rather than an unnecessarily complicated system.
