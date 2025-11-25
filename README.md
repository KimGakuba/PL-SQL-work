# **👤 Student Profile**  

🔹 **NAME:** NGABONZIZA Kim Gakuba  
🔹 **ID:** `27670`  
🔹 **GROUP:**  **D** 
🔹Course: *Database Development with PL/SQL (INSY 831)*
🔹Instructor: **Eric Maniraguha**


---

# 📘 Hospital Emergency Room Patient Queue (PL/SQL Project)

---

## 📌 Project Overview

This PL/SQL project simulates how a **Hospital Emergency Room** manages patient information.
The system records patient symptoms, priority level, and basic details.

The project demonstrates three key PL/SQL concepts:

* **Collections (VARRAY)**
* **Records (User-defined composite type)**
* **GOTO statements (Control flow handling)**

---

## 🎯 Problem Statement

In a busy hospital emergency department, nurses must record patient information as soon as they arrive.

Each patient has:

* Patient ID
* Full Name
* Priority Level (High, Medium, Low)
* A list of up to **5 symptoms**

Your system should:

1. Use a **VARRAY** to store patient symptoms
2. Use a **Record** to store patient data
3. Count the number of symptoms
4. Skip processing with a **GOTO** if no symptoms were recorded
5. Print full patient details

---

## 🧠 Concepts Demonstrated

### 🔹 1. **VARRAY Collection**

Used to store a maximum of 5 symptoms:

```sql
TYPE SymptomList IS VARRAY(5) OF VARCHAR2(50);
```

### 🔹 2. **Record**

Used to group patient details and symptoms:

```sql
TYPE PatientRec IS RECORD (
    patient_id NUMBER,
    patient_name VARCHAR2(60),
    priority_level VARCHAR2(10),
    symptoms SymptomList
);
```

### 🔹 3. **GOTO Statement**

Used to jump to an error-handling label:

```sql
GOTO no_symptoms;
```

---

## 🧱 Full PL/SQL Code

```sql
SET SERVEROUTPUT ON;

DECLARE
  -- 1. Symptoms collection (VARRAY)
  TYPE SymptomList IS VARRAY(5) OF VARCHAR2(50);

  -- 2. Patient record
  TYPE PatientRec IS RECORD (
    patient_id NUMBER,
    patient_name VARCHAR2(60),
    priority_level VARCHAR2(10),
    symptoms SymptomList
  );

  -- 3. Variables
  patient PatientRec;
  symptom_count NUMBER := 0;

BEGIN
  -- 4. Assign patient info
  patient.patient_id := 501;
  patient.patient_name := 'NGABONZIZA Kim';
  patient.priority_level := 'High';
  patient.symptoms := SymptomList('Headache', 'Fever', 'Chest Pain');

  -- 5. Check if symptoms exist
  IF patient.symptoms.COUNT = 0 THEN
    GOTO no_symptoms;
  END IF;

  -- 6. Count symptoms
  symptom_count := patient.symptoms.COUNT;

  -- 7. Display patient details
  DBMS_OUTPUT.PUT_LINE('Patient Name: ' || patient.patient_name);
  DBMS_OUTPUT.PUT_LINE('Priority Level: ' || patient.priority_level);
  DBMS_OUTPUT.PUT_LINE('Number of Reported Symptoms: ' || symptom_count);

  DBMS_OUTPUT.PUT_LINE('Symptoms List:');
  FOR i IN 1..patient.symptoms.COUNT LOOP
    DBMS_OUTPUT.PUT_LINE('- ' || patient.symptoms(i));
  END LOOP;

  GOTO end_program;

  -- 8. Label for missing symptoms
  <<no_symptoms>>
  DBMS_OUTPUT.PUT_LINE('Error: No symptoms recorded for this patient.');

  -- 9. End program label
  <<end_program>>
  DBMS_OUTPUT.PUT_LINE('Emergency room check completed.');

END;
/
```

---

## 🖥️ Example Output

### ✔️ Case 1: Patient has symptoms

```
Patient Name: NGABONZIZA Kim
Priority Level: High
Number of Reported Symptoms: 3
Symptoms List:
- Headache
- Fever
- Chest Pain
Emergency room check completed.
```

#### 1. Screenshot of output  
![Inserting Data into customers](https://github.com/KimGakuba/PL-SQL-work/blob/main/screenshots/output.png)

---
#### 2. Screenshot of records  
![Inserting Data into customers](https://github.com/KimGakuba/PL-SQL-work/blob/main/screenshots/record.png)

---


### ❌ Case 2: No symptoms entered

```
Error: No symptoms recorded for this patient.
Emergency room check completed.
```

---


---

## 📚 Conclusion

This project clearly demonstrates:

* How to use **VARRAY collections**
* How to group data using **Records**
* How to manage program flow with **GOTO**
* How PL/SQL can model real-world hospital operations


---

