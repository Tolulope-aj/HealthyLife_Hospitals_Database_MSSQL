# HealthyLife Hospitals Database Management System

### Project Overview
The HealthyLife Hospitals Database Management System is designed to efficiently manage anad analyze patient admissions, diagnoses, wards and related informations. This comprehensive database system aims to streamline hospital operations, improve patient care, and provide valuable insights into hospital performance.

### Database Structure
The database consists of the following core tables:

Patient: Stores patient demographic information, including Patient ID, Forename, Surname, Date of birth, Gender, Postcode.
Admission: Records patient admissions, including admission and discharge dates, specialty code, ward code, diagnosis code, gp code, gppractice code and admission method.
Specialty: Lists available medical specialties (e.g., Cardiology, Neurology).
Ward: Details hospital wards and their type (e.g., ICU, General).
MethodOfAdmission: Defines different admission methods (e.g., Elective, Emergency).
Diagnosis: Describes different medical diagnoses used for patient records (e.g., Malaria, Dengue fever).
GP: Stores information about general practitioners 
GPPractice: Lists GP practices.
These tables are interconnected through foreign key relationships to maintain data integrity and enable efficient querying.

### Data Population
The database is populated with sample data to simulate real-world scenarios. Data is inserted into each table using SQL `INSERT` statements. The data includes information about 
