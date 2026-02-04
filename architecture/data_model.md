```mermaid
erDiagram
    %% CITIZEN Entity - The core user
    CITIZEN {
        string NINO PK "National Insurance Number"
        string first_name
        string last_name
        date dob "Date of Birth"
        string address_postcode
    }

    %% CLAIM Entity - The application for a benefit
    CLAIM {
        string claim_id PK
        string NINO FK "Links to Citizen"
        date submission_date
        string status "New, Processing, Approved, Rejected"
        float requested_amount
    }

    %% BENEFIT_TYPE Entity - e.g., Universal Credit, PIP
    BENEFIT_TYPE {
        string benefit_code PK
        string benefit_name
        string department_owner
    }

    %% APPOINTMENT Entity - Assessment booking
    APPOINTMENT {
        string appt_id PK
        string claim_id FK
        date appt_date
        string outcome "Attended, DNA, Rescheduled"
    }

    %% Relationships
    CITIZEN ||--o{ CLAIM : "submits"
    CLAIM }|--|| BENEFIT_TYPE : "is_for"
    CLAIM ||--o{ APPOINTMENT : "requires"
