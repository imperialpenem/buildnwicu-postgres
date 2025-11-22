NWICU Database Schema
======================================================================================================================================================

| Schema   | Table           | Variable                 | Type                  | Index                 | Primary Keys       | Foreign Keys                  | References                    |
|:---------|:----------------|:-------------------------|:----------------------|:----------------------|:-------------------|:------------------------------|:------------------------------|
| nw_hosp  | admissions      | subject_id               | INTEGER NOT NULL      | admissions_idx01      | nan                | admissions_patients_fk        | nw_hosp.patients (subject_id) |
| nw_hosp  | admissions      | hadm_id                  | INTEGER NOT NULL      | admissions_idx01      | admissions_pk      | nan                           | nan                           |
| nw_hosp  | admissions      | admittime                | TIMESTAMP NOT NULL    | admissions_idx01      | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | dischtime                | TIMESTAMP             | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | deathtime                | TIMESTAMP             | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | admission_type           | VARCHAR(40)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | admit_provider_id        | VARCHAR(10)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | admission_location       | VARCHAR(60)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | discharge_location       | VARCHAR(100)          | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | insurance                | VARCHAR(100)          | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | language                 | VARCHAR(25)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | marital_status           | VARCHAR(30)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | race                     | VARCHAR(80)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | edregtime                | TIMESTAMP             | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | edouttime                | TIMESTAMP             | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | admissions      | hospital_expire_flag     | SMALLINT              | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | d_icd_diagnoses | icd_code                 | CHAR(7) NOT NULL      | nan                   | d_icd_diagnoses_pk | nan                           | nan                           |
| nw_hosp  | d_icd_diagnoses | icd_version              | SMALLINT NOT NULL     | nan                   | d_icd_diagnoses_pk | nan                           | nan                           |
| nw_hosp  | d_icd_diagnoses | long_title               | VARCHAR(255)          | D_ICD_DIAG_idx02      | nan                | nan                           | nan                           |
| nw_hosp  | d_labitems      | itemid                   | INTEGER NOT NULL      | nan                   | d_labitems_pk      | nan                           | nan                           |
| nw_hosp  | d_labitems      | label                    | VARCHAR(50)           | d_labitems_idx01      | nan                | nan                           | nan                           |
| nw_hosp  | d_labitems      | fluid                    | VARCHAR(50)           | d_labitems_idx01      | nan                | nan                           | nan                           |
| nw_hosp  | d_labitems      | category                 | VARCHAR(50)           | d_labitems_idx01      | nan                | nan                           | nan                           |
| nw_hosp  | diagnoses_icd   | subject_id               | INTEGER NOT NULL      | nan                   | nan                | diagnoses_icd_patients_fk     | nw_hosp.patients (subject_id) |
| nw_hosp  | diagnoses_icd   | hadm_id                  | INTEGER NOT NULL      | nan                   | diagnoses_icd_pk   | diagnoses_icd_admissions_fk   | nw_hosp.admissions (hadm_id)  |
| nw_hosp  | diagnoses_icd   | seq_num                  | INTEGER NOT NULL      | nan                   | diagnoses_icd_pk   | nan                           | nan                           |
| nw_hosp  | diagnoses_icd   | icd_code                 | CHAR(7)               | nan                   | diagnoses_icd_pk   | nan                           | nan                           |
| nw_hosp  | diagnoses_icd   | icd_version              | SMALLINT              | nan                   | diagnoses_icd_pk   | nan                           | nan                           |
| nw_hosp  | emar            | subject_id               | INTEGER NOT NULL      | nan                   | nan                | emar_patients_fk              | nw_hosp.patients (subject_id) |
| nw_hosp  | emar            | hadm_id                  | INTEGER               | nan                   | nan                | emar_admissions_fk            | nw_hosp.admissions (hadm_id)  |
| nw_hosp  | emar            | emar_id                  | VARCHAR(25) NOT NULL  | nan                   | emar_pk            | nan                           | nan                           |
| nw_hosp  | emar            | emar_seq                 | INTEGER NOT NULL      | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | emar            | poe_id                   | VARCHAR(25) NOT NULL  | emar_idx01            | nan                | nan                           | nan                           |
| nw_hosp  | emar            | pharmacy_id              | INTEGER               | emar_idx02            | nan                | nan                           | nan                           |
| nw_hosp  | emar            | enter_provider_id        | VARCHAR(10)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | emar            | charttime                | TIMESTAMP NOT NULL    | emar_idx03            | nan                | nan                           | nan                           |
| nw_hosp  | emar            | medication               | TEXT                  | emar_idx04            | nan                | nan                           | nan                           |
| nw_hosp  | emar            | event_txt                | VARCHAR(100)          | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | emar            | scheduletime             | TIMESTAMP             | emar_idx03            | nan                | nan                           | nan                           |
| nw_hosp  | emar            | storetime                | TIMESTAMP NOT NULL    | emar_idx03            | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | labevent_id              | INTEGER NOT NULL      | nan                   | labevents_pk       | nan                           | nan                           |
| nw_hosp  | labevents       | subject_id               | INTEGER NOT NULL      | nan                   | nan                | labevents_patients_fk         | nw_hosp.patients (subject_id) |
| nw_hosp  | labevents       | hadm_id                  | INTEGER               | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | specimen_id              | INTEGER               | labevents_idx02       | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | itemid                   | INTEGER NOT NULL      | nan                   | nan                | labevents_d_labitems_fk       | nw_hosp.d_labitems (itemid)   |
| nw_hosp  | labevents       | order_provider_id        | VARCHAR(10)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | charttime                | TIMESTAMP(0)          | labevents_idx01       | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | storetime                | TIMESTAMP(0)          | labevents_idx01       | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | value                    | VARCHAR(200)          | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | valuenum                 | DOUBLE PRECISION      | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | valueuom                 | VARCHAR(20)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | ref_range_lower          | DOUBLE PRECISION      | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | ref_range_upper          | DOUBLE PRECISION      | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | flag                     | VARCHAR(10)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | priority                 | VARCHAR(7)            | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | labevents       | comments                 | TEXT                  | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | patients        | subject_id               | INTEGER NOT NULL      | nan                   | patients_pk        | nan                           | nan                           |
| nw_hosp  | patients        | gender                   | CHAR(1) NOT NULL      | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | patients        | anchor_age               | SMALLINT              | patients_idx01        | nan                | nan                           | nan                           |
| nw_hosp  | patients        | anchor_year              | SMALLINT NOT NULL     | patients_idx02        | nan                | nan                           | nan                           |
| nw_hosp  | patients        | anchor_year_group        | VARCHAR(20) NOT NULL  | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | patients        | dod                      | DATE                  | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | subject_id               | INTEGER NOT NULL      | nan                   | nan                | prescriptions_patients_fk     | nw_hosp.patients (subject_id) |
| nw_hosp  | prescriptions   | hadm_id                  | INTEGER NOT NULL      | nan                   | nan                | prescriptions_admissions_fk   | nw_hosp.admissions (hadm_id)  |
| nw_hosp  | prescriptions   | pharmacy_id              | INTEGER NOT NULL      | nan                   | prescriptions_pk   | nan                           | nan                           |
| nw_hosp  | prescriptions   | poe_id                   | VARCHAR(25)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | poe_seq                  | INTEGER               | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | order_provider_id        | VARCHAR(10)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | starttime                | TIMESTAMP(3)          | prescriptions_idx01   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | stoptime                 | TIMESTAMP(3)          | prescriptions_idx01   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | drug_type                | VARCHAR(80)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | drug                     | VARCHAR(255) NOT NULL | nan                   | prescriptions_pk   | nan                           | nan                           |
| nw_hosp  | prescriptions   | formulary_drug_cd        | VARCHAR(50)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | gsn                      | VARCHAR(255)          | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | ndc                      | VARCHAR(25)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | prod_strength            | VARCHAR(255)          | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | form_rx                  | VARCHAR(25)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | dose_val_rx              | VARCHAR(100)          | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | dose_unit_rx             | VARCHAR(50)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | form_val_disp            | VARCHAR(255)          | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | form_unit_disp           | VARCHAR(50)           | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | doses_per_24_hrs         | REAL                  | nan                   | nan                | nan                           | nan                           |
| nw_hosp  | prescriptions   | route                    | VARCHAR(50)           | nan                   | nan                | nan                           | nan                           |
| nw_icu   | chartevents     | subject_id               | INTEGER NOT NULL      | nan                   | nan                | chartevents_patients_fk       | nw_hosp.patients (subject_id) |
| nw_icu   | chartevents     | hadm_id                  | INTEGER NOT NULL      | nan                   | nan                | chartevents_admissions_fk     | nw_hosp.admissions (hadm_id)  |
| nw_icu   | chartevents     | stay_id                  | INTEGER NOT NULL      | nan                   | nan                | chartevents_icustays_fk       | nw_icu.icustays (stay_id)     |
| nw_icu   | chartevents     | caregiver_id             | INTEGER               | nan                   | nan                | nan                           | nan                           |
| nw_icu   | chartevents     | charttime                | TIMESTAMP NOT NULL    | chartevents_idx01     | nan                | nan                           | nan                           |
| nw_icu   | chartevents     | storetime                | TIMESTAMP             | chartevents_idx01     | nan                | nan                           | nan                           |
| nw_icu   | chartevents     | itemid                   | INTEGER NOT NULL      | nan                   | nan                | chartevents_d_items_fk        | nw_icu.d_items (itemid)       |
| nw_icu   | chartevents     | value                    | VARCHAR(200)          | nan                   | nan                | nan                           | nan                           |
| nw_icu   | chartevents     | valuenum                 | FLOAT                 | nan                   | nan                | nan                           | nan                           |
| nw_icu   | chartevents     | valueuom                 | VARCHAR(20)           | nan                   | nan                | nan                           | nan                           |
| nw_icu   | chartevents     | warning                  | SMALLINT              | nan                   | nan                | nan                           | nan                           |
| nw_icu   | d_items         | itemid                   | INTEGER NOT NULL      | nan                   | d_items_pk         | nan                           | nan                           |
| nw_icu   | d_items         | label                    | VARCHAR(255) NOT NULL | d_items_idx01         | nan                | nan                           | nan                           |
| nw_icu   | d_items         | abbreviation             | VARCHAR(50)           | d_items_idx01         | nan                | nan                           | nan                           |
| nw_icu   | d_items         | linksto                  | VARCHAR(30) NOT NULL  | nan                   | nan                | nan                           | nan                           |
| nw_icu   | d_items         | category                 | VARCHAR(50)           | d_items_idx02         | nan                | nan                           | nan                           |
| nw_icu   | d_items         | unitname                 | VARCHAR(50)           | nan                   | nan                | nan                           | nan                           |
| nw_icu   | d_items         | param_type               | VARCHAR(20) NOT NULL  | nan                   | nan                | nan                           | nan                           |
| nw_icu   | d_items         | lownormalvalue           | FLOAT                 | nan                   | nan                | nan                           | nan                           |
| nw_icu   | d_items         | highnormalvalue          | FLOAT                 | nan                   | nan                | nan                           | nan                           |
| nw_icu   | icustays        | subject_id               | INTEGER NOT NULL      | nan                   | nan                | icustays_patients_fk          | nw_hosp.patients (subject_id) |
| nw_icu   | icustays        | hadm_id                  | INTEGER NOT NULL      | nan                   | nan                | icustays_admissions_fk        | nw_hosp.admissions (hadm_id)  |
| nw_icu   | icustays        | stay_id                  | INTEGER NOT NULL      | nan                   | icustays_pk        | nan                           | nan                           |
| nw_icu   | icustays        | first_careunit           | VARCHAR(50)           | icustays_idx01        | nan                | nan                           | nan                           |
| nw_icu   | icustays        | last_careunit            | VARCHAR(50)           | icustays_idx01        | nan                | nan                           | nan                           |
| nw_icu   | icustays        | intime                   | TIMESTAMP             | icustays_idx02        | nan                | nan                           | nan                           |
| nw_icu   | icustays        | outtime                  | TIMESTAMP             | icustays_idx02        | nan                | nan                           | nan                           |
| nw_icu   | icustays        | los                      | FLOAT                 | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | subject_id               | INTEGER NOT NULL      | nan                   | nan                | procedureevents_patients_fk   | nw_hosp.patients (subject_id) |
| nw_icu   | procedureevents | hadm_id                  | INTEGER NOT NULL      | nan                   | nan                | procedureevents_admissions_fk | nw_hosp.admissions (hadm_id)  |
| nw_icu   | procedureevents | stay_id                  | INTEGER NOT NULL      | nan                   | nan                | procedureevents_icustays_fk   | nw_icu.icustays (stay_id)     |
| nw_icu   | procedureevents | caregiver_id             | INTEGER               | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | starttime                | TIMESTAMP NOT NULL    | procedureevents_idx01 | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | endtime                  | TIMESTAMP             | procedureevents_idx01 | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | storetime                | TIMESTAMP             | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | itemid                   | INTEGER NOT NULL      | nan                   | nan                | procedureevents_d_items_fk    | nw_icu.d_items (itemid)       |
| nw_icu   | procedureevents | value                    | FLOAT                 | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | valueuom                 | VARCHAR(20)           | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | location                 | VARCHAR(100)          | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | locationcategory         | VARCHAR(50)           | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | orderid                  | INTEGER               | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | linkorderid              | INTEGER               | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | ordercategoryname        | VARCHAR(50)           | procedureevents_idx02 | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | ordercategorydescription | VARCHAR(30)           | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | patientweight            | FLOAT                 | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | isopenbag                | SMALLINT              | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | continueinnextdept       | SMALLINT              | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | statusdescription        | VARCHAR(50)           | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | originalamount           | FLOAT                 | nan                   | nan                | nan                           | nan                           |
| nw_icu   | procedureevents | originalrate             | FLOAT                 | nan                   | nan                | nan                           | nan                           |
