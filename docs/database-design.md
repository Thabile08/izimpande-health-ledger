# Izimpande Health Ledger - Database Design

## Overview

This document describes the database structure for Izimpande Health Ledger.

The system uses a relational database (MySQL) to manage users, health records, medications, appointments, institutions, and audit logs.

---

# Entity Relationship Overview

Users
|
+-- Patients
|
+-- Health Records
|
+-- Medications
|
+-- Appointments
|
+-- Audit Logs

Institutions
|
+-- Patients

---

# Table: roles

Purpose:
Stores system roles.

Fields:

* id (PK)
* role_name

Example Values:

* ADMIN
* HEALTHCARE_WORKER
* CAREGIVER
* PATIENT

---

# Table: users

Purpose:
Stores account information.

Fields:

* id (PK)
* first_name
* last_name
* email
* password
* phone_number
* role_id (FK)
* created_at
* updated_at

---

# Table: institutions

Purpose:
Stores institutions supported by the system.

Fields:

* id (PK)
* institution_name
* institution_type
* address
* contact_number
* email

Institution Types:

* RURAL_CLINIC
* OLD_AGE_HOME
* ORPHANAGE
* CORRECTIONAL_FACILITY

---

# Table: patients

Purpose:
Stores patient information.

Fields:

* id (PK)
* user_id (FK)
* institution_id (FK)
* date_of_birth
* gender
* blood_type
* allergies
* emergency_contact_name
* emergency_contact_number

---

# Table: health_records

Purpose:
Stores diagnoses and treatment history.

Fields:

* id (PK)
* patient_id (FK)
* diagnosis
* treatment_plan
* notes
* recorded_by
* record_date

---

# Table: medications

Purpose:
Stores medication information.

Fields:

* id (PK)
* patient_id (FK)
* medication_name
* dosage
* frequency
* start_date
* end_date

---

# Table: appointments

Purpose:
Stores appointment information.

Fields:

* id (PK)
* patient_id (FK)
* institution_id (FK)
* appointment_date
* appointment_status
* notes

Status Values:

* SCHEDULED
* COMPLETED
* CANCELLED

---

# Table: audit_logs

Purpose:
Maintains the ledger history.

Fields:

* id (PK)
* user_id (FK)
* action
* entity_name
* entity_id
* timestamp

Example Actions:

* CREATE_RECORD
* UPDATE_RECORD
* DELETE_RECORD
* LOGIN
* BOOK_APPOINTMENT

---

# Future Tables

## vaccinations

Tracks patient vaccinations.

## wellness_metrics

Tracks:

* Weight
* Blood Pressure
* Glucose Levels
* BMI

## notifications

Tracks reminders and alerts.

---

# Database Relationships

users -> roles

patients -> users

patients -> institutions

health_records -> patients

medications -> patients

appointments -> patients

appointments -> institutions

audit_logs -> users
