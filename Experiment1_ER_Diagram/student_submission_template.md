# ER Diagram Submission - VISWAJITH LALITHRAM R.V - 212224240187

## Scenario Chosen:
Hospital

## ER Diagram:
![Screenshot 2025-03-06 144502](https://github.com/user-attachments/assets/a6e9f56a-9498-4631-87cf-afb694a2b3d9)


## Entities and Attributes:

1. PATIENT
Attributes:
PATIENT_ID (Primary Key)
NAME
AGE
HEALTH
DIABETES

2. APPOINTMENTS
Attributes:
APP_ID (Primary Key)
APP_DATETIME
FEES

3. DOCTOR
Attributes:
DOC_ID (Primary Key)
NAME
SPECIALIZATION

4. DEPARTMENT
Attributes:
DEPT_ID (Primary Key)
NAME
NUMBER



## Relationships and Constraints:

1. Book (between PATIENT and APPOINTMENTS)
Cardinality: One patient can book many appointments; each appointment is booked by one patient.
Participation: Total participation from APPOINTMENTS (every appointment must be booked by a patient).

2. Assign (between APPOINTMENTS and DOCTOR)
Cardinality: One appointment is assigned to one doctor; a doctor can have many appointments.
Participation: Total for APPOINTMENTS.

3. Assign (between DOCTOR and DEPARTMENT)
Cardinality: One doctor belongs to one department; one department can have many doctors.
Participation: Total for DOCTOR.


## Extension (Prerequisite / Billing):

Billing: The FEES attribute in APPOINTMENTS represents billing information. You could extend this by adding a BILLING entity with attributes like BILL_ID, PAYMENT_STATUS, etc., and link it to APPOINTMENTS.

Prerequisite: If modeling treatment dependencies or referrals, a new relationship or entity (e.g., TREATMENT or REFERRAL) could be added connecting doctors and specific procedures


## Design Choices:

Normalization: Each major concept (Patient, Doctor, Department, Appointment) is treated as an entity to maintain data integrity.

Scalability: The relationships allow expansion—e.g., a patient can book multiple appointments, and doctors can serve multiple patients.

Clarity: Color-coded entities and clear role-based relationships help keep the model readable and logical.

Practical use case: Matches real-world hospital management scenarios with booking, assigning, and department organization.
