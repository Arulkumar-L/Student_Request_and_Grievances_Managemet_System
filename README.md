````md
# Student Service Hub

### ServiceNow-based Student Self-Service & Request Management System

> A ServiceNow scoped application that provides students with a centralized self-service portal to submit and track Leave, On-Duty (OD), and Grievance requests, while automating approvals, notifications, assignments, and role-based access.

---

## 📌 Overview

The **KIOT Student Service Hub** is a ServiceNow-based application designed to digitize common student administrative processes.

Traditionally, students may need to write physical letters and obtain approvals/signatures from multiple faculty members such as:

- Mentor
- Class Advisor
- Head of Department (HOD)
- Warden for hostellers

This process can be time-consuming and difficult to track.

The application provides a centralized **Student Self-Service Portal** where students can:

- Apply for Leave
- Apply for On-Duty (OD)
- Raise Grievances
- Track submitted requests
- View approval status
- Receive approval/rejection notifications

Faculty and administrators can process requests through role-based interfaces.

---

# 🎯 Objectives

The main objectives of the project are:

- Digitize student Leave and OD request processes.
- Automate multi-level approval workflows.
- Provide a centralized grievance management system.
- Provide students with a self-service experience.
- Allow students to track their requests.
- Notify students about approval/rejection decisions.
- Implement role-based access and record security.
- Demonstrate practical ServiceNow CSA and CAD concepts.
- Learn ServiceNow application development through a real-world use case.

---

# 🏗️ Application Architecture

```text
                         KIOT STUDENT
                              │
                              ▼
                ┌──────────────────────────┐
                │   KIOT STUDENT PORTAL    │
                │     Service Portal       │
                └────────────┬─────────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
        Leave Request     OD Request     Grievance
              │              │              │
              └──────────────┼──────────────┘
                             │
                             ▼
                  ServiceNow Application
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
        Flow Designer    Notifications   Security
              │
              ▼
        Approval Process
              │
       ┌──────┼─────────┐
       ▼      ▼         ▼
    Mentor  Advisor    HOD
                         │
                  Hosteller?
                    /       \
                  Yes        No
                   │          │
                Warden      Complete
                   │
                   ▼
               Final Status
````

---

# 🧩 Main Modules

## 1. Student Management

Stores basic student information required by the application.

### Example information

* Student
* Register Number
* Department
* Year
* Section
* Accommodation Type
* Mentor
* Class Advisor

The Student Profile is referenced by Leave, OD, and Grievance records.

---

## 2. Leave Management

Students can submit Leave requests through the Student Portal.

### Leave Request fields

* Number
* Student
* Leave Type
* From Date
* To Date
* Reason
* Attachment
* Status
* Current Approver
* Rejection Reason
* Created
* Updated

### Leave Types

* Casual Leave
* Medical Leave
* Emergency Leave
* Other

### Approval Flow

```text
Student submits Leave
        │
        ▼
      Mentor
        │
        ▼
  Class Advisor
        │
        ▼
       HOD
        │
        ▼
   Is Hosteller?
      /     \
    Yes      No
     │        │
  Warden      │
     │        │
     └────┬───┘
          ▼
       Approved
```

If any required approver rejects the request:

```text
Reject
  │
  ▼
Request Status = Rejected
  │
  ▼
Store Rejection Reason
  │
  ▼
Notify Student
```

---

# 3. On-Duty (OD) Management

Students can apply for On-Duty permission for activities such as:

* Hackathons
* Symposiums
* Workshops
* Competitions
* Conferences
* College events
* Other approved activities

### OD Request fields

* Number
* Student
* Event / Activity Name
* Organization
* From Date
* To Date
* Reason
* Location
* Attachment
* Status
* Current Approver
* Rejection Reason
* Created
* Updated

The approval process is similar to Leave requests.

---

# 4. Grievance Management

Students can raise grievances from the Student Portal.

### Example categories

* Academic
* Hostel
* Infrastructure
* Placement
* Transport
* Examination
* Other

### Grievance fields

* Number
* Student
* Category
* Subject
* Description
* Priority
* Status
* Assigned To
* Resolution
* Attachment
* Created
* Updated

### Grievance lifecycle

```text
New
 │
 ▼
Assigned
 │
 ▼
In Progress
 │
 ▼
Resolved
 │
 ▼
Closed
```

Unlike Leave and OD, grievances use an **assignment and resolution process** rather than a multi-level approval workflow.

---

# 🌐 Student Self-Service Portal

Students interact with the application through a dedicated **Service Portal** instead of directly accessing backend tables.

### Portal features

* Apply for Leave
* Apply for OD
* Raise Grievance
* My Requests
* My Leave Requests
* My OD Requests
* My Grievances
* Request status tracking

### Example Portal

```text
--------------------------------------------------
              KIOT STUDENT SERVICES
--------------------------------------------------

Welcome, Student

[ Apply Leave ]     [ Apply OD ]

[ Raise Grievance ]

--------------------------------------------------
MY REQUESTS

Leave       Pending: 2
OD          Approved: 1
Grievance   In Progress: 1

--------------------------------------------------
RECENT REQUESTS

LV000123     Leave       Pending
OD000045     OD          Approved
GR000021     Grievance   In Progress
--------------------------------------------------
```

---

# 📋 Request Tracking

Students can track their submitted requests through the portal.

Example:

```text
Leave Request: LV000123

Status: Pending

Mentor          ✓ Approved
Class Advisor   ● Pending
HOD             ○ Waiting
Warden          ○ Not Required
```

---

# 👥 Role-Based Experiences

The application uses ServiceNow roles and access controls to provide appropriate functionality to different users.

## Student

Can:

* Submit Leave requests
* Submit OD requests
* Raise Grievances
* View own requests
* Track request status

## Mentor / Faculty

Can:

* View assigned requests
* Approve Leave requests
* Approve OD requests
* Reject requests with a reason

## HOD

Can:

* View relevant department requests
* Approve/reject Leave requests
* Approve/reject OD requests

## Warden

Can:

* View hosteller requests requiring Warden approval
* Approve/reject applicable requests

## Administrator

Can:

* Manage application data
* Manage users/roles
* Manage master data
* Monitor application records
* View reports and dashboards

---

# 🔐 Security

The application implements ServiceNow security concepts such as:

* Roles
* Groups
* ACLs
* Record-level access
* Application scope

The goal is to ensure that students cannot access other students' requests.

For example:

```text
Student A
   ↓
Can view Student A's requests

Student B
   ↓
Can view Student B's requests
```

Faculty, HOD, Warden, and administrators receive access according to their responsibilities.

---

# ⚙️ ServiceNow Concepts Demonstrated

This project is designed as a practical learning project covering major ServiceNow CSA and CAD concepts.

## Configuration

* Scoped Application
* Application Menu
* Modules
* Tables
* Fields
* Reference Fields
* Choice Fields
* Forms
* Lists
* Views
* Users
* Groups
* Roles
* ACLs
* UI Policies
* Data Policies
* Notifications
* Flow Designer
* Reports
* Dashboards
* Service Portal

## Development

* JavaScript
* Client Scripts
* GlideForm
* GlideRecord
* GlideSystem
* Script Includes
* GlideAjax
* Business Rules
* Events
* Server-side scripting
* Client-side scripting
* Debugging and logging

## Data Management

* Data Sources
* Import Sets
* Import Set Tables
* Transform Maps
* Field Mapping
* Coalesce
* Transform Scripts

## Deployment

* Scoped Application
* Application versions
* Application Repository
* Update Sets
* Instance-to-instance deployment concepts

---

# 🔄 Flow Designer

Flow Designer is used to automate Leave and OD approval processes.

### Example

```text
Trigger:
Leave Request Created
        │
        ▼
Get Student Information
        │
        ▼
Determine Mentor
        │
        ▼
Mentor Approval
        │
    ┌───┴────┐
    │        │
 Approved   Rejected
    │        │
    ▼        ▼
Advisor    Reject
Approval
    │
    ▼
HOD Approval
    │
    ▼
Check Accommodation
    │
 ┌──┴────┐
 │       │
Hosteller Day Scholar
 │       │
 ▼       │
Warden   │
Approval │
 │       │
 └───┬───┘
     ▼
 Approved
     │
     ▼
Notify Student
```

---

# 📧 Notifications

The application sends notifications at important stages.

### Student

* Request submitted
* Request approved
* Request rejected
* Rejection reason

### Approver

* New request requiring approval

Example:

```text
Subject:
Leave Request LV000123 Requires Your Approval

Student:
Arulkumar L

Leave Dates:
10-Aug-2026 to 11-Aug-2026

Reason:
Personal work

Please review the request.
```

# 📥 Data Import

Student/faculty master data can be loaded using ServiceNow Import Sets.

### Process

```text
CSV File
   │
   ▼
Data Source
   │
   ▼
Import Set Table
   │
   ▼
Transform Map
   │
   ▼
Target Table
```

Concepts demonstrated:

* Data Source
* Import Set
* Import Set Table
* Transform Map
* Field Mapping
* Coalesce
* Transform Scripts

---

# 🚀 Application Deployment

The application is developed inside a **ServiceNow scoped application**.

Application deployment and configuration migration are treated separately.

## Application Repository

For supported organizational instances, the scoped application can be published as a versioned application package.

```text
Development Instance
        │
        ▼
KIOT Student Service Hub
        │
        ▼
Publish Application Version
        │
        ▼
Application Repository
        │
        ▼
Entitled Target Instance
        │
        ▼
Install Application
```

Example versions:

```text
1.0.0
 ├── Student Management
 ├── Leave Management
 └── Basic Portal

1.1.0
 ├── OD Management
 ├── Grievance Management
 └── Notifications

2.0.0
 ├── Reports
 ├── Dashboard
 └── Improved Security
```

> Application Repository availability and entitlement depend on the ServiceNow instance and organization configuration.

---

# 🔄 Update Sets

Update Sets are also studied as part of the project's ServiceNow development and deployment learning.

Typical process:

```text
Development Instance
        │
        ▼
Create Update Set
        │
        ▼
Make Configuration Changes
        │
        ▼
Complete Update Set
        │
        ▼
Transfer to Target Instance
        │
        ▼
Preview
        │
        ▼
Commit
```

Update Sets are not treated as a replacement for the scoped application's deployment mechanism. They are learned separately for moving applicable configuration changes between instances.

---

# 🧪 Testing

Testing is performed after implementing each module.

## Leave Testing

| Test Case             | Expected Result               |
| --------------------- | ----------------------------- |
| Valid Leave request   | Request created               |
| Invalid date range    | Submission prevented          |
| Mentor approves       | Moves to next approval        |
| Mentor rejects        | Request rejected              |
| All approvers approve | Leave approved                |
| Hosteller             | Warden approval included      |
| Day Scholar           | Warden approval skipped       |
| Rejection             | Student receives notification |

## OD Testing

| Test Case              | Expected Result      |
| ---------------------- | -------------------- |
| Valid OD request       | Request created      |
| Missing required field | Submission prevented |
| Approver approves      | Moves to next stage  |
| Approver rejects       | Request rejected     |
| All approvals complete | OD approved          |
| Rejection              | Student notified     |

## Grievance Testing

| Test Case           | Expected Result            |
| ------------------- | -------------------------- |
| Valid grievance     | Grievance created          |
| Missing description | Submission prevented       |
| Assignment          | Assigned staff can process |
| Status update       | Student can track status   |
| Resolution          | Student receives update    |
| Closure             | Grievance marked closed    |

---

# 🛠️ Development Approach

The project follows a phased development approach.

```text
Phase 1
Requirements & Architecture
        ↓
Phase 2
Scoped Application Foundation
        ↓
Phase 3
Student & Master Data
        ↓
Phase 4
Leave Management
        ↓
Phase 5
OD Management
        ↓
Phase 6
Grievance Management
        ↓
Phase 7
Service Portal
        ↓
Phase 8
Flow Designer & Notifications
        ↓
Phase 9
Security & ACLs
        ↓
Phase 10
Scripting & CAD Concepts
        ↓
Phase 11
Import Sets
        ↓
Phase 12
Reports & Dashboard
        ↓
Phase 13
Testing
        ↓
Phase 14
Deployment & Documentation
```

---

# 🧠 Learning Objectives

While developing this project, the following concepts are studied practically:

### CSA

* ServiceNow platform fundamentals
* Application and scope
* Tables and data model
* Forms and lists
* Users, groups and roles
* Access control
* Service Portal
* Flow Designer
* Notifications
* Reports and dashboards
* Data import
* Update Sets

### CAD

* JavaScript
* Client-side scripting
* Server-side scripting
* GlideForm
* GlideRecord
* GlideSystem
* Script Includes
* GlideAjax
* Business Rules
* Application development
* Scoped APIs
* Debugging
* Application deployment

---

# 🧰 Technology Stack

| Technology             | Purpose                         |
| ---------------------- | ------------------------------- |
| ServiceNow             | Application platform            |
| Service Portal         | Student self-service experience |
| Flow Designer          | Approval automation             |
| JavaScript             | Application scripting           |
| Glide API              | ServiceNow server/client APIs   |
| Import Sets            | Data migration                  |
| Reports & Dashboards   | Data visualization              |
| ACLs & Roles           | Security                        |
| Application Repository | Application deployment          |

---

# 📸 Screenshots

Screenshots will be added as the application is developed.

Planned screenshots:

* **Student Portal Homepage**
  <img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/3ffa5ad6-2ffe-4c79-a1da-f871e5aee207" />

* **Apply Leave Form**
  <img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/fda6b8f1-025e-43e8-b6df-77affaf918d8" />

* **Apply OD Form**
  <img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/f82b90bf-d80c-40de-a74d-8535efcc6cce" />

* **Grievance Form**
  <img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/fcbd8485-3680-4aa1-b261-c9c3182f8f77" />

* **My Requests**
  <img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/60790321-6231-4f2c-a4c3-51a1a1e505f4" />

* **Leave Approval Flow of student request**
  <img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/345b4f76-02b6-4806-a722-7fafb992d0cb" />

* **OD Approval Flow of student request**
  <img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/d741ef44-b81c-469e-9e1b-f452e57c3858" />

* **Grievance Approval Flow of student request**
  <img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/913e1282-e866-4c90-ae3d-dd4bb1bcdebb" />

* **Faculty, HOD, Mentor, Warden Approval View**
 <img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/f97eca68-af38-47c3-93c9-83e6870ba1c4" />

* **Application Scope & Application Repository**
  <img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/449a3bfd-007a-4dd9-8d1c-6e021e516c72" />

---

# 🚀 How to Import and Run in a New ServiceNow PDI

Follow these steps to import this scoped application into a new Personal Developer Instance (PDI).

---

## 📋 Prerequisites
- Active ServiceNow PDI (Washington DC / Xanadu or later).
- GitHub Personal Access Token (Classic) with repo read/write permissions.

---

## 🔗 Step 1: Link Application from Source Control
1. Log in to your ServiceNow instance as **System Administrator**.
2. Navigate to: **System Applications → Studio**.
3. In the Application Explorer modal, click **Import From Source Control**.
4. Configure the Git repository connection:
   - **URL:** `https://github.com/<your-username>/<your-repo-name>.git`
   - **Branch:** `sn_instances/dev442413`
   - **Credential:** Create/Select a Basic Auth credential using your GitHub Username and GitHub Personal Access Token (PAT) as the password.
5. Click **Import**.  
   Studio will pull all metadata, tables, forms, widgets, and business logic into your instance.

---

## ⚙️ Step 2: Configure Service Portal Routing
1. In the main ServiceNow navigation bar, search for **Service Portal → Portals**.
2. Locate and open the portal record:  
   **Student Request Management System**  
   *(URL Suffix: `student_services` or `kiot`)*
3. Ensure the **Homepage** field is set to:  
   `student_request_home_page`
4. Click **Update**.

---

## 🌐 Step 3: Access the Portal
Open your browser and navigate to:
  https://<YOUR-NEW-INSTANCE-NAME>.service-now.com/student_services
---

## 🧪 Testing Personas & Validation Scenarios

| Persona              | Configuration Setup                                                                 | Expected Portal Experience                                                                 |
|----------------------|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| **Student (Day Scholar)** | Record in `student_profile` with `accommodation_type = Day Scholar`                  | Sees **Apply Leave / OD / Grievance** cards; Tracker sets Warden to **Not Required**.       |
| **Student (Hosteller)**   | Record in `student_profile` with `accommodation_type = Hosteller`                     | Approval Tracker enforces **4-tier chain** including Hostel Warden.                         |
| **Faculty (Advisor / Mentor / HOD)** | `sys_user` record referenced in `mentor`, `class_advisor`, or `hod` fields          | Sees **Staff Approval Center** with pending queues and approve/reject actions.              |
| **Hostel Warden**         | `sys_user` record referenced in `warden` field                                        | Sees queue of hosteller requests passed by the HOD.                                         |

---

# 🔮 Future Improvements

The current project intentionally focuses on a manageable feature set.

Possible future improvements include:

* Mobile-friendly experience
* Advanced approval configuration
* SLA-based grievance handling
* Escalation mechanisms
* Advanced analytics
* Integration with external college systems
* Automated academic calendar integration
* Attendance integration
* Advanced notification preferences

These features are outside the initial project scope.

---

# 🎓 Project Scope

This project is designed as a **learning and portfolio project** rather than a production enterprise implementation.

The primary goals are:

1. Understand ServiceNow platform concepts.
2. Practice CSA concepts.
3. Practice CAD concepts.
4. Build a realistic ServiceNow application.
5. Understand configuration vs customization.
6. Learn Flow Designer and Service Portal.
7. Understand ServiceNow security.
8. Learn application deployment concepts.
9. Develop a project that can be demonstrated in technical interviews.

---

# 💡 Key Learning Outcome

The main objective is not simply to create a working application.

The objective is to understand **why each ServiceNow component is used and how the components work together**.

For example:

```text
Student
   ↓
Service Portal
   ↓
Record / Request
   ↓
Flow Designer
   ↓
Approval
   ↓
Business Logic
   ↓
Notification
   ↓
Student Tracking
```

This project provides practical exposure to how ServiceNow can be used to transform a traditional manual process into a structured digital workflow.

---
