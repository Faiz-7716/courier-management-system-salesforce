# Courier Management System (CMS) - Salesforce Cloud

**Developer:** Mohammed Faiz P.  
**Institution:** Mazharul Uloom College  
**Program:** TN Skills – Vetri Thiran Payarchi Thittam (VTPT)  

## 📌 Project Overview
Courier and logistics companies often struggle to efficiently manage shipments and deliveries due to manual processes and disconnected systems. The Courier Management System (CMS) is a cloud-based logistics solution built entirely on the Salesforce platform. It centralizes shipment booking, real-time tracking, delivery agent assignment, automated status updates, billing, and performance analytics.

## 🚀 Technology Stack
*   **Platform:** Salesforce Developer Edition
*   **User Interface:** Salesforce Lightning Experience
*   **Data Model:** Custom Objects (Customer, Shipment, Delivery Agent, Branch, Delivery Update, Invoice)
*   **Automation:** Record-Triggered Flows, Validation Rules
*   **Security:** Role-Based Access Control (Profiles, Roles)
*   **Analytics:** Lightning Reports & Dashboards

## 📂 Repository Structure

*   📁 **1. Brainstorming & Ideation:** Problem Statement and Empathy Maps.
*   📁 **2. Requirement Analysis:** Customer Journey, Functional & Non-Functional Requirements.
*   📁 **3. Project Design Phase:** Solution Architecture and Data Flow Diagrams.
*   📁 **4. Project Planning Phase:** Agile Sprint Schedule and Product Backlog.
*   📁 **5. Project Development Phase:** Schema Builder, Object Configurations, and Flow layouts.
*   📁 **6. Project Testing:** Functional test cases and Salesforce execution screenshots.
*   📁 **7. Project Documentation:** Final comprehensive project report.
*   📁 **8. Project Demonstration:** Link to the live video walkthrough of the Salesforce implementation.

## ⚙️ Key Features Implemented
1.  **Data Validation:** Strict rules preventing invalid data entry (e.g., ensuring 10-digit phone numbers and valid package weights).
2.  **Automated Status Sync:** A Salesforce Flow that automatically updates the master Shipment status when a Delivery Agent logs a new tracking update.
3.  **Security & Hierarchy:** Custom profiles ensuring Branch Managers, Delivery Agents, and Customer Support only see the data relevant to their roles.
4.  **Live Analytics:** Real-time dashboards tracking revenue by branch, agent performance, and package transit statuses.
