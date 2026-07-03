

1. What tables would your database need to contain?
 
Patients, Doctors, Staff, Appointments, Trusts, Billing, Departments, Staff, Test results, Contractors, Prescriptions, Medications.
 
2. Which table will BECOME the largest over time?
 
Patients, Appointments, Medical Records.
 
3. What 5 searches do you think will happen most frequently on your DB?
 
Patients_id, Staff, Test results, Appointment_availability, Patients_History.
 
4. What data do you think would be most important and why?
 
**Patients(DATA)** (Medical records), Doctors, Trusts, Departments, appointments
 
- Patient Data contain all the importment info via medical history, diagnosis etc.

```mermaid
erDiagram

    ORGANISATION {
        int organisation_id PK
        string organisation_name
        string organisation_type
        string website
    }

    DEPARTMENT {
        int department_id PK
        int organisation_id FK
        string department_name
    }

    LOCATION {
        int location_id PK
        string site_name
        string city
        string county
        string postcode
        string region
        string country
    }

    OCCUPATION {
        int occupation_id PK
        string category
        string specialty
        string nhs_band
    }

    JOB {
        int job_id PK
        string reference_number
        string job_title
        text job_description
        string contract_type
        string working_pattern
        string employment_type
        date posted_date
        date closing_date
        string status
        int organisation_id FK
        int department_id FK
        int location_id FK
        int occupation_id FK
        int salary_id FK
    }

    SALARY {
        int salary_id PK
        decimal minimum_salary
        decimal maximum_salary
        string salary_type
        string pay_band
    }

    RECRUITER {
        int recruiter_id PK
        string name
        string email
        string phone
    }

    JOB_CONTACT {
        int job_id FK
        int recruiter_id FK
        string contact_type
    }

    APPLICANT {
        int applicant_id PK
        string first_name
        string last_name
        string email
    }

    APPLICATION {
        int application_id PK
        int applicant_id FK
        int job_id FK
        datetime application_date
        string status
        decimal score
    }

    ORGANISATION ||--o{ DEPARTMENT : contains
    ORGANISATION ||--o{ JOB : advertises

    DEPARTMENT ||--o{ JOB : owns
    LOCATION ||--o{ JOB : located_at
    OCCUPATION ||--o{ JOB : classified_as
    SALARY ||--o{ JOB : offers

    JOB ||--o{ JOB_CONTACT : has
    RECRUITER ||--o{ JOB_CONTACT : manages

    APPLICANT ||--o{ APPLICATION : submits
    JOB ||--o{ APPLICATION : receives
```