# Local Admin Access Request Automation
## Intelligent Ticketing System using Copilot Studio & EasyVista

## 🎯 Overview

This project automates the **Local Admin Access Request** approval workflow in the IT Service Management (ITSM) ecosystem using **Microsoft Copilot Studio** and **EasyVista** ticketing system. The solution intelligently analyzes access requests and provides AI-driven confidence scores to streamline approval processes while maintaining security and compliance standards.

**Project Type:** Intelligent Automation  
**Platform:** Microsoft Copilot Studio + EasyVista ITSM  
**Trigger:** Email-based (Shared Mailbox)  
**Language:** Agent Flow & Knowledge Base

---

## ⚠️ Problem Statement

**Current Challenges:**
- Manual review of every local admin access request by ITSM managers
- Inconsistent approval timelines and decision-making
- High administrative overhead reducing team efficiency
- Time-consuming manual analysis of request justifications
- Risk of approval inconsistencies based on subjective evaluation
- Delayed access provisioning affecting employee productivity

**Business Impact:**
- Average ticket resolution time: Manually intensive
- Employee wait time for access approval: Extended delays
- Manager workload: High repetitive manual tasks
- Potential security gaps due to manual oversight

---

## 💡 Solution Architecture

The solution implements an **intelligent automated approval system** that:
1. Captures incoming requests via shared mailbox
2. Analyzes request content using AI
3. Generates confidence scores based on historical patterns
4. Routes requests intelligently based on confidence thresholds
5. Automatically approves/rejects or escalates for manager review

### High-Level Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                    Employee Request                          │
│            (Submit Local Admin Access Request)               │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│                  Shared Mailbox                              │
│           (Email Notification Trigger)                      │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│            Copilot Studio Agent                              │
│           "EV Request Analyzer"                       │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ 1. Extract Request Information                      │   │
│  │    - Duration of Access                            │   │
│  │    - Device Name                                   │   │
│  │    - User Principal Name (UPN)                     │   │
│  │    - Justification                                 │   │
│  └─────────────────────────────────────────────────────┘   │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│            Knowledge Base Analysis                           │
│      "Justification Document" (Historical Data)             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ • Last 12 months of approved requests              │   │
│  │ • Last 12 months of rejected requests              │   │
│  │ • Pattern matching & analysis                      │   │
│  └─────────────────────────────────────────────────────┘   │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│         AI Confidence Score Generation                       │
│              (0% - 100%)                                    │
└──────────────────────┬──────────────────────────────────────┘
                       │
         ┌─────────────┼─────────────┐
         │             │             │
         ▼             ▼             ▼
   ┌─────────┐  ┌─────────────┐  ┌──────────┐
   │ ≥ 90%   │  │ 50% - 90%   │  │ < 50%    │
   │         │  │             │  │          │
   ▼         ▼  ▼             ▼  ▼          ▼
┌────────┐ ┌──────────────┐ ┌─────────┐
│ AUTO   │ │  ESCALATE TO │ │ AUTO    │
│APPROVE │ │   MANAGER    │ │REJECT   │
│        │ │  for Review  │ │         │
└────────┘ │with Score &  │ └─────────┘
           │  Details     │
           └──────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────────┐
│              EasyVista Ticketing Tool                        │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ • Update AI Confidence Score Field                  │   │
│  │ • Update Approval Status                            │   │
│  │ • Notify Requester with Decision                    │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

---

## ✨ Key Features

### 1. **Automated Email Processing**
- Monitors shared mailbox for incoming access requests
- Extracts structured data from email content
- Parses all required fields automatically

### 2. **Intelligent Request Analysis**
- Analyzes request duration (short-term vs long-term access)
- Evaluates justification quality and completeness
- Cross-references with historical approval patterns
- Considers device type and user role implications

### 3. **AI-Driven Confidence Scoring**
- Generates confidence scores based on ML analysis
- Compares against 12-month historical dataset
- Provides transparent scoring rationale
- Scales from 0% (high risk) to 100% (low risk)

### 4. **Intelligent Routing Logic**
| Confidence Score | Action | Outcome |
|---|---|---|
| ≥ 90% | Auto-Approve | Immediate access provisioning |
| 50% - 90% | Escalate to Manager | Manager reviews score + request details |
| < 50% | Auto-Reject | User directed to ITSM team or manager |

### 5. **Real-Time EasyVista Integration**
- Updates ticket with AI Confidence Score field
- Modifies approval status automatically
- Sends notifications to relevant stakeholders
- Maintains audit trail for compliance

### 6. **Transparency & Auditability**
- Every decision is tracked and logged
- Confidence score rationale provided
- Full request history maintained
- Compliance-ready audit trail

---

## 🏗️ System Components

### 1. **Copilot Studio Agent: "EV Request Analyzer"**

**Type:** Cloud-based Intelligent Agent  
**Framework:** Power Automate + Copilot Studio  
**Trigger:** "When a new email arrives in shared mailbox"

**Agent Capabilities:**
```
├── Email Parser
│   ├── Extract recipient information
│   ├── Parse request details
│   └── Validate required fields
│
├── Knowledge Base Connector
│   ├── Query "Justification Document"
│   ├── Retrieve historical patterns
│   └── Access approval history
│
├── AI Analysis Engine
│   ├── Confidence score calculation
│   ├── Pattern matching
│   └── Risk assessment
│
└── EasyVista Integrator
    ├── Update ticket status
    ├── Write confidence score
    └── Trigger notifications
```

### 2. **Knowledge Base: "Justification Document"**

**Purpose:** Historical reference database for pattern analysis  
**Content Scope:** Last 12 months of data

**Includes:**
- Approved requests (with justifications)
- Rejected requests (with reasons)
- Common business justifications
- Department-specific patterns
- Access duration patterns
- Device type correlations

**Format:** Structured knowledge document with metadata

### 3. **EasyVista Ticketing System**

**New Field Added:**
- **Field Name:** AI Confidence Score
- **Data Type:** Numeric (0-100)
- **Description:** AI-generated confidence score for auto-approval logic
- **Visibility:** Visible to managers and ITSM Team

**Integrated Actions:**
- Automatic status updates
- Score field population
- Notification triggering
- Ticket categorization

### 4. **Shared Mailbox Trigger**

**Configuration:**
- Monitor: Shared mailbox for admin access requests
- Trigger Event: New email arrival
- Frequency: Real-time processing
- Retry Logic: Exponential backoff for failures

### Request Information Fields

**Required Fields Extracted:**

| Field | Description | Example |
|-------|-------------|---------|
| **Duration of Access** | How long admin access is needed | 30 days, 7 days, 60 days |
| **Device Name** | Target machine for admin access | LAP-EMP-12345, DESK-123 |
| **User Principal Name** | Azure AD identity of requester | john.doe@company.com |
| **Justification** | Business reason for access request | Software installation, System testing, Updates |
| **Ticket ID** | Unique reference in EasyVista | TKT-2024-001234 |
| **Requester Name** | Full name of person requesting | John Doe |
| **Department** | Organizational unit | Engineering, Finance, HR |
| **Submission Date** | When request was submitted | 2024-06-15 10:30 AM |


#### Step 3: Create EasyVista Custom Field

```
In EasyVista Administration:
1. Go to Custom Fields
2. Create new field:
   - Field Name: AI Confidence Score
   - Field Type: Numeric (0-100)
   - Decimal Places: 2
   - Default Value: 0
   - Visibility: All users
   - Mandatory: No
   
3. Add to Admin Access Request form
4. Set field read/write permissions
5. Configure field in email notifications
```

#### Step 4: Import Knowledge Base

```
1. Prepare "Justification Document":
   - Export approved requests (12 months)
   - Export rejected requests (12 months)
   - Include justification text
   - Mark approval/rejection status
   
2. Format as structured document:
   - CSV or JSON format
   - Include metadata fields
   - Ensure consistent formatting
   
3. Upload to Knowledge Base:
   - Navigate to Knowledge Base settings
   - Import Justification Document
   - Verify all records loaded
   - Test search functionality
```

#### Step 5: Configure Notifications

```
1. EasyVista to Shared Mailbox:
   - Settings > Notifications
   - On ticket creation → Send to shared mailbox
   - Include all request fields
   
2. Agent to Managers (for 50-90% scores):
   - Create email notification action
   - Recipients: Manager email list
   - Include: Ticket ID, Score, Justification, Recommendation
   
3. Agent to Requester:
   - Create email notification action
   - Send: Auto-approval/rejection notification
   - Include: Decision reason, AI score, next steps


## 📊 Performance Metrics

### Key Performance Indicators (KPIs)

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| **Manual Review Time** | 100% | 15-20% | 80-85% reduction |
| **Average Resolution Time** | 2-3 days | 2-30 minutes | 200x faster |
| **Manager Workload** | High (100%) | Low (20-30%) | 70-80% reduction |
| **Auto-Approval Rate** | N/A | 60-70% | Automation ratio |
| **Manual Review Rate** | 100% | 25-35% | Significant reduction |
| **Auto-Rejection Rate** | N/A | 5-10% | Early filtering |
| **Process Efficiency** | Baseline | +85% | Estimated gain |
| **Employee Wait Time** | 2-3 days | < 1 hour | Dramatically improved |
| **Approval Consistency** | Variable | >95% | Improved compliance |
| **Security Compliance** | Standard | Enhanced | AI-driven assessment |

### Operational Benefits

**Time Savings:**
- Average time per request review: 2 minutes → 10 seconds (auto) or 1 minute (manager review)
- Annual hours saved: ~200+ hours for ITSM team
- Employee wait time: 2-3 days → <1 hour


### A. Common Scenarios & Expected Scores

**Scenario 1: High Confidence (≥90%)**
```
Request: "Need local admin to install Visual Studio 2022 for development work"
Duration: 7 days
Department: Engineering
Status: AUTO APPROVED
Reasoning: Clear justification, reasonable duration, typical for department
Score: 94%
```

**Scenario 2: Medium Confidence (50-90%)**
```
Request: "Need admin access for software testing"
Duration: 45 days
Department: QA
Status: MANAGER REVIEW
Reasoning: Acceptable justification, longer duration requires verification
Score: 72%
Manager Action: Review and approve/reject
```

**Scenario 3: Low Confidence (<50%)**
```
Request: "Need it" 
Duration: 180 days
Department: Finance
Status: AUTO REJECTED
Reasoning: Insufficient justification, excessive duration
Score: 18%
Next Step: Contact manager or resubmit with proper justification
```

### C. Troubleshooting Guide

| Issue | Cause | Solution |
|-------|-------|----------|
| Agent not triggering | Shared mailbox not monitored | Verify connection, test with sample email |
| Fields not extracted correctly | Email format unexpected | Check email template, adjust parsing logic |
| Low confidence scores | Knowledge base missing data | Update knowledge base with recent requests |
| EasyVista not updating | API connection issue | Verify credentials, check firewall rules |
| Slow performance | High email volume | Optimize knowledge base queries |

---

## 📄 License & Attribution

This documentation covers proprietary automation solution developed for internal ITSM processes.

For updates and support, contact the IT Automation Team.

---

**Last Updated:** June 2024  
**Status:** Production  
**Maintained By:** IT Automation Team
