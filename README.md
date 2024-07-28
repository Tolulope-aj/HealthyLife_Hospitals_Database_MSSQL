# HealthyLife Hospitals Database Management System

## Table of Contents
- [Project Overview](#project-overview)
- [Database Schema](#database-schema)
- [Tool](#tool)
- [Database Design](#database-design)
- [Data Population](#data-population)
- [Queries and Analysis](#queries-and-analysis)

### Project Overview
The HealthyLife Hospitals Database Management System is designed to efficiently manage anad analyze patient admissions, diagnoses, wards and related informations. This comprehensive database system aims to streamline hospital operations, improve patient care, and provide valuable insights into hospital performance.

### Database Schema
The database schema consists of the following tables:

- Patient: Stores patient demographic information, including Patient ID, Forename, Surname, Date of birth, Gender, Postcode.

- Admission: Records patient admissions, including admission and discharge dates, specialty code, ward code, diagnosis code, gp code, gppractice code and admission method.

- Specialty: Lists available medical specialties (e.g., Cardiology, Neurology).

- Ward: Details hospital wards and their type (e.g., ICU, General).

- MethodOfAdmission: Defines different admission methods (e.g., Elective, Emergency).

- Diagnosis: Describes different medical diagnoses used for patient records (e.g., Malaria, Dengue fever).

- GP: Stores information about general practitioners.

- GPPractice: Lists GP practices.

These tables are interconnected through foreign key relationships to maintain data integrity and enable efficient querying.

### Tool 
- Database Management System (DBMS): Microsoft SQL Server.

### Database Design
```sql
-- Database Implementation Project: HealthyLife Hospitals
-- Create a database for Healthylife Hospitals

CREATE DATABASE Healthylife_Hospitals;
USE Healthylife_Hospitals;


-- Create tables in the Healthylife_Hospitals Database

-- Create Patient table	
CREATE TABLE Patient (
    PatientID INT IDENTITY(101,1) PRIMARY KEY,
    Forename NVARCHAR(50) NOT NULL,
    Surname NVARCHAR(50) NOT NULL,
    DateOfBirth DATE NOT NULL,
    Gender NVARCHAR(10) NOT NULL,
    Postcode NVARCHAR(10) NOT NULL
);
SELECT *
FROM Patient;

-- Create Specialty table
CREATE TABLE Specialty (
    SpecialtyCode NVARCHAR(10) PRIMARY KEY,
    SpecialtyName NVARCHAR(100) NOT NULL
);
SELECT *
FROM Specialty;

-- Create Ward table
CREATE TABLE Ward (
    WardCode NVARCHAR(10) PRIMARY KEY,
    WardName NVARCHAR(100) NOT NULL,
    WardType NVARCHAR(50) NOT NULL
);
SELECT *
FROM Ward;

-- Create MethodOfAdmission table
CREATE TABLE MethodOfAdmission (
    MethodOfAdmissionCode NVARCHAR(10) PRIMARY KEY,
    MethodOfAdmissionType NVARCHAR(50) NOT NULL
);
SELECT *
FROM MethodOfAdmission;

-- Create Admission table
CREATE TABLE Admission (
    AdmissionID INT IDENTITY(1001,1) PRIMARY KEY,
    PatientID INT NOT NULL,
    SpecialtyCode NVARCHAR(10) NOT NULL,
    WardCode NVARCHAR(10) NOT NULL,
	LengthOfStay INT NOT NULL,				
	AdmissionDate DATE NOT NULL,
    DischargeDate DATE,
    MethodOfAdmissionCode NVARCHAR(10) NOT NULL,
	DiagnosisCode NVARCHAR(10) NOT NULL,
	GPPracticeCode NVARCHAR(10) NOT NULL,
    FOREIGN KEY (PatientID) REFERENCES Patient(PatientID),
    FOREIGN KEY (SpecialtyCode) REFERENCES Specialty(SpecialtyCode),
    FOREIGN KEY (WardCode) REFERENCES Ward(WardCode),
    FOREIGN KEY (MethodOfAdmissionCode) REFERENCES MethodOfAdmission(MethodOfAdmissionCode),
	FOREIGN KEY (DiagnosisCode) REFERENCES Diagnosis(DiagnosisCode),
	FOREIGN KEY (GPPracticeCode) REFERENCES GPPractice(GPPracticeCode)
);
SELECT *
FROM Admission;

-- Create Diagnosis table
CREATE TABLE Diagnosis (
    DiagnosisCode NVARCHAR(10) PRIMARY KEY,				
    DiagnosisDescription NVARCHAR(255) NOT NULL
);
SELECT *
FROM Diagnosis;

-- Create GPPractice table
CREATE TABLE GPPractice (
    GPPracticeCode NVARCHAR(10) PRIMARY KEY,
    PracticeName NVARCHAR(100) NOT NULL,
    PracticePostcode NVARCHAR(10) NOT NULL
);
SELECT *
FROM GPPractice;

-- Create GP table
CREATE TABLE GP (
    GPCode NVARCHAR(10) PRIMARY KEY,
    GPName NVARCHAR(100) NOT NULL,
    GPPracticeCode NVARCHAR(10) NOT NULL,
    FOREIGN KEY (GPPracticeCode) REFERENCES GPPractice(GPPracticeCode)
);
SELECT *
FROM GP;
```
### Data Population
The database is populated with realistic sample data for testing and analysis. This includes creating a substantial number of records for patients, admissions and diagnoses to simulate real-world scenarios. Data is inserted into each table using SQL `INSERT` statements.
```sql
-- DATA POPULATION
-- Populate the tables with realistic sample data.
-- Insert data into Patient Table

INSERT INTO Patient (Forename, Surname, DateOfBirth, Gender, Postcode)
VALUES ('John', 'Doe', '1980-01-15', 'Male', 'SK2'),
('Jane', 'Smith', '1990-02-20', 'Female', 'SK2'),
('Michael', 'Johnson', '1975-03-25', 'Male', 'SK2'),
('Emily', 'Davis', '1985-04-30', 'Female', 'SK2'),
('Olivia', 'Brown', '1995-05-10', 'Female', 'SK2'),
('William', 'Jones', '1988-06-15', 'Male', 'SK2'),
('Sophia', 'Garcia', '1992-07-20', 'Female', 'SK2'),
('James', 'Martinez', '1983-08-25', 'Male', 'SK2'),
('Isabella', 'Rodriguez', '1997-09-30', 'Female', 'SK1'),
('Benjamin', 'Wilson', '1981-10-05', 'Male', 'SK2'),
('Mia', 'Anderson', '1993-11-10', 'Female', 'SK3'),
('Lucas', 'Thomas', '1986-12-15', 'Male', 'SK2'),
('Charlotte', 'Taylor', '1998-01-20', 'Female', 'SK2'),
('Henry', 'Moore', '1982-02-25', 'Male', 'SK2'),
('Amelia', 'Jackson', '1994-03-30', 'Female', 'SK2'),
('Alexander', 'White', '1987-04-05', 'Male', 'SK5'),
('Ava', 'Harris', '1991-05-10', 'Female', 'SK2'),
('Daniel', 'Martin', '1984-06-15', 'Male', 'SK2'),
('Evelyn', 'Thompson', '1996-07-20', 'Female', 'SK2'),
('Matthew', 'Martinez', '1989-08-25', 'Male', 'SK3'),
('Harper', 'Clark', '1999-09-30', 'Female', 'SK2'),
('David', 'Lewis', '1985-10-05', 'Male', 'SK2'),
('Ella', 'Walker', '1992-11-10', 'Female', 'SK2'),
('Joseph', 'Hall', '1983-12-15', 'Male', 'SK2'),
('Grace', 'Allen', '1995-01-20', 'Female', 'SK1'),
('Samuel', 'Young', '1988-02-25', 'Male', 'SK2'),
('Lily', 'Hernandez', '1997-03-30', 'Female', 'SK2'),
('Andrew', 'King', '1981-04-05', 'Male', 'SK2'),
('Hannah', 'Wright', '1993-05-10', 'Female', 'SK2'),
('Christopher', 'Lopez', '1986-06-15', 'Male', 'SK2'),
('Zoe', 'Hill', '1998-07-20', 'Female', 'SK2'),
('Joshua', 'Scott', '1984-08-25', 'Male', 'SK2'),
('Natalie', 'Green', '1996-09-30', 'Female', 'SK2'),
('Ryan', 'Adams', '1987-10-05', 'Male', 'SK2'),
('Leah', 'Baker', '1991-11-10', 'Female', 'SK2'),
('Nathan', 'Gonzalez', '1985-12-15', 'Male', 'SK2'),
('Aubrey', 'Nelson', '1999-01-20', 'Female', 'SK2'),
('Isaac', 'Carter', '1989-02-25', 'Male', 'SK2'),
('Sofia', 'Mitchell', '1994-03-30', 'Female', 'SK2'),
('Caleb', 'Perez', '1982-04-05', 'Male', 'SK2'),
('Victoria', 'Roberts', '1995-05-10', 'Female', 'SK3'),
('Christian', 'Turner', '1983-06-15', 'Male', 'SK2'),
('Aria', 'Phillips', '1997-07-20', 'Female', 'SK2'),
('Jonathan', 'Campbell', '1986-08-25', 'Male', 'SK1'),
('Layla', 'Parker', '1992-09-30', 'Female', 'SK2'),
('Dylan', 'Evans', '1988-10-05', 'Male', 'SK2'),
('Chloe', 'Edwards', '1993-11-10', 'Female', 'SK2'),
('Gabriel', 'Collins', '1981-12-15', 'Male', 'SK2'),
('Scarlett', 'Stewart', '1996-01-20', 'Female', 'SK2'),
('Anthony', 'Sanchez', '1984-02-25', 'Male', 'SK2'),
('Penelope', 'Morris', '1998-03-30', 'Female', 'SK2'),
('Jack', 'Rogers', '1987-04-05', 'Male', 'SK2'),
('Riley', 'Reed', '1991-05-10', 'Female', 'SK7'),
('Owen', 'Cook', '1985-06-15', 'Male', 'SK2'),
('Chinwe', 'Okafor', '1990-03-05', 'Female', 'SK2'),
('Emeka', 'Nwosu', '1982-04-10', 'Male', 'SK2'),
('Amina', 'Bello', '1978-05-15', 'Female', 'SK1'),
('Tunde', 'Adebayo', '1986-06-20', 'Male', 'SK2'),
('Ngozi', 'Eze', '1991-07-25', 'Female', 'SK2'),
('Ifeanyi', 'Obi', '1993-08-30', 'Male', 'SK2'),
('Fatima', 'Ajala', '1984-09-05', 'Female', 'SK2'),
('Bola', 'Ogun', '1995-10-10', 'Male', 'SK1'),
('Kemi', 'Akin', '1987-11-15', 'Female', 'SK2'),
('Chidi', 'Uche', '1992-12-20', 'Male', 'SK1'),
('Ada', 'Nnamdi', '1983-01-25', 'Female', 'SK2'),
('Yemi', 'Ojo', '1994-02-28', 'Male', 'SK2'),
('Zainat', 'Ali', '1985-03-05', 'Female', 'SK2'),
('Kunle', 'Balogun', '1996-04-10', 'Male', 'SK2'),
('Aisha', 'Mohammed', '1988-05-15', 'Female', 'SK2'),
('Gbenga', 'Adetokunbo', '1997-06-20', 'Male', 'SK2'),
('Halima', 'Usman', '1989-07-25', 'Female', 'SK1'),
('Femi', 'Ade', '1990-08-30', 'Male', 'SK6'),
('Nkechi', 'Onye', '1981-09-05', 'Female', 'SK2'),
('Sule', 'Yusuf', '1993-10-10', 'Male', 'SK2'),
('Bisi', 'Ola', '1982-11-15', 'Female', 'SK2'),
('Uche', 'Chukwu', '1994-12-20', 'Male', 'SK2'),
('Amaka', 'Ike', '1986-01-25', 'Female', 'SK2'),
('Tayo', 'Olu', '1995-02-06', 'Male', 'SK2'),
('Maryam', 'Kano', '1987-03-05', 'Female', 'SK2'),
('Segun', 'Ola', '1998-04-10', 'Male', 'SK2'),
('Nafisat', 'Baba', '1983-05-15', 'Female', 'SK2'),
('Bayo', 'Ogun', '1996-06-20', 'Male', 'SK2'),
('Khadija', 'Sani', '1984-07-25', 'Female', 'SK2'),
('Ibrahim', 'Abdullahi', '1997-08-30', 'Male', 'SK2'),
('Chinyere', 'Okeke', '1985-09-05', 'Female', 'SK2'),
('Musa', 'Garba', '1999-10-10', 'Male', 'SK2'),
('Oluchi', 'Nwankwo', '1988-11-15', 'Female', 'SK2'),
('Seyi', 'Ogun', '1991-12-20', 'Male', 'SK2'),
('Zainab', 'Bello', '1986-01-25', 'Female', 'SK2'),
('Chukwuma', 'Eze', '1993-02-03', 'Male', 'SK2'),
('Amina', 'Saheed', '1987-03-05', 'Female', 'SK2'),
('Tunde', 'Adebayo', '1995-04-10', 'Male', 'SK2'),
('Ngozi', 'Eze', '1989-05-15', 'Female', 'SK2'),
('Ifeanyi', 'Obi', '1992-06-20', 'Male', 'SK2'),
('Fatima', 'Abubakar', '1984-07-25', 'Female', 'SK2'),
('Bola', 'Ogun', '1996-08-30', 'Male', 'SK2'),
('Kemi', 'Akin', '1985-09-05', 'Female', 'SK3'),
('Chidi', 'Uche', '1997-10-10', 'Male', 'SK1'),
('Ada', 'Nnamdi', '1983-11-15', 'Female', 'SK2'),
('Yemi', 'Ojo', '1994-12-20', 'Male', 'SK2'),
('Zainab', 'Ali', '1986-01-25', 'Female', 'SK2'),
('Kunle', 'Balogun', '1995-02-12', 'Male', 'SK3'),
('Aisha', 'Mohammed', '1987-03-05', 'Female', 'SK2'),
('Gbenga', 'Adetokunbo', '1998-04-10', 'Male', 'SK2'),
('Halima', 'Usman', '1984-05-15', 'Female', 'SK2'),
('Femi', 'Ade', '1996-06-20', 'Male', 'SK6'),
('Nkechi', 'Onye', '1985-07-25', 'Female', 'SK8'),
('Sule', 'Yusuf', '1997-08-30', 'Male', 'SK1'),
('Bisi', 'Ola', '1983-09-05', 'Female', 'SK2'),
('Uche', 'Chukwu', '1995-10-10', 'Male', 'SK2'),
('Amaka', 'Ike', '1981-11-15', 'Female', 'SK2'),
('Tayo', 'Olu', '1993-12-20', 'Male', 'SK2'),
('Maryam', 'Kano', '1984-01-25', 'Female', 'SK2'),
('Segun', 'Ola', '1996-02-21', 'Male', 'SK2'),
('Nafisat', 'Baba', '1987-03-05', 'Female', 'SK2'),
('Bayo', 'Ogun', '1998-04-10', 'Male', 'SK2'),
('Khadija', 'Sani', '1985-05-15', 'Female', 'SK4'),
('Ibrahim', 'Abdullahi', '1997-06-20', 'Male', 'SK6'),
('Chinyere', 'Okeke', '1983-07-25', 'Female', 'SK2'),
('Musa', 'Garba', '1995-08-30', 'Male', 'SK1'),
('Oluchi', 'Nwankwo', '1984-09-05', 'Female', 'SK2'),
('Seyi', 'Ogun', '1996-10-10', 'Male', 'SK2'),
('Kaimat', 'Bello', '1986-11-15', 'Female', 'SK5'),
('Chukwuma', 'Eze', '1998-12-20', 'Male', 'SK8'),
('Amina', 'Abubakar', '1985-01-25', 'Female', 'SK2'),
('Tunde', 'Adebayo', '1997-02-28', 'Male', 'SK1'),
('Ngozi', 'Eze', '1983-03-05', 'Female', 'SK2'),
('Ifeanyi', 'Obi', '1995-04-10', 'Male', 'SK2'),
('Busayo', 'Abubakar', '1984-05-15', 'Female', 'SK7'),
('Bola', 'Ogun', '1996-06-20', 'Male', 'SK2');

SELECT *
FROM Patient;

-- Insert data into Specialty Table

INSERT INTO Specialty (SpecialtyCode, SpecialtyName)
VALUES ('CA01', 'Cardiology'),
('NE02', 'Neurology'),
('OR03', 'Orthopedics'),
('DE04', 'Dermatology'),
('PS05', 'Psychiatry'),
('ON06', 'Oncology'),
('PE07', 'Pediatrics'),
('GE08', 'Geriatrics'),
('OB09', 'Obstetrics'),
('EN10', 'Endocrinology'),
('GA11', 'Gastroenterology'),
('HE12', 'Hematology'),
('IN13', 'Infectious Diseases'),
('NE14', 'Nephrology'),
('PU15', 'Pulmonology'),
('RH16', 'Rheumatology'),
('SU17', 'Surgery'),
('UR18', 'Urology'),
('OP19', 'Ophthalmology'),
('OT20', 'Otolaryngology'),
('AN21', 'Anesthesiology'),
('IM22', 'Internal Medicine'),
('FM23', 'Family Medicine'),
('AI24', 'Allergy and Immunology'),
('PR25', 'Physical Medicine and Rehabilitation'),
('EM26', 'Emergency Medicine');

SELECT *
FROM Specialty;

-- Insert data into Ward Table

INSERT INTO Ward (WardCode, WardName, WardType)
VALUES ('ICU', 'Intensive Care Unit', 'Critical Care'),
       ('GEN', 'General Ward', 'Medical/Surgical'),
       ('ENDO', 'Endoscopy Suite', 'Procedural'),
       ('CARDIO', 'Cardiology Ward', 'Cardiac Care'),
       ('RESP', 'Respiratory Ward', 'Pulmonary Care'),
       ('NEURO', 'Neurology Ward', 'Neurological Care'),
       ('OBGYN', 'Obstetrics & Gynecology Ward', 'Women''s Health'),
       ('PEDS', 'Pediatrics Ward', 'Children''s Health'),
       ('ORTHO', 'Orthopedics Ward', 'Musculoskeletal Care'),
       ('PSYCH', 'Psychiatry Ward', 'Mental Health'),
	     ('ER', 'Emergency Room', 'Urgent Care'),
       ('IMC', 'Intermediate Care Unit', 'Step-Down Care'),
       ('NICU', 'Neonatal Intensive Care Unit', 'Critical Care for Newborns'),
       ('REHAB', 'Rehabilitation Ward', 'Recovery and Physical Therapy'),
       ('ONC', 'Oncology Ward', 'Cancer Care'),
       ('NEPH', 'Nephrology Ward', 'Kidney Care'),
       ('GAS', 'Gastroenterology Ward', 'Digestive Care'),
       ('URO', 'Urology Ward', 'Urinary Tract Care'),
       ('BURNS', 'Burns Unit', 'Specialized Burn Care'),
       ('ISO', 'Isolation Ward', 'Infectious Disease Care'),
       ('MATERNITY', 'Maternity Ward', 'Delivery and Postpartum Care'),
       ('PREOP', 'Pre-operative Ward', 'Preparation for Surgery'),
       ('POSTOP', 'Post-operative Ward', 'Recovery After Surgery'),
	     ('HEMATO', 'Hematology Ward', 'Blood Disorders'),
       ('INF', 'Infectious Disease Ward', 'Treatment of Contagious Diseases'),
       ('TXPLANT', 'Transplant Unit', 'Organ Transplant Care'),
       ('DIALYSIS', 'Dialysis Unit', 'Kidney Failure Treatment'),
       ('WALK-IN', 'Walk-In Clinic', 'Minor Injuries and Illnesses');

SELECT *
FROM Ward;

-- Insert data into GPPractice Table

INSERT INTO GPPractice (GPPracticeCode, PracticeName, PracticePostcode)
VALUES ('GPP001', 'Central City Medical Practice', 'SK1'),
       ('GPP002', 'Riverside Health Centre', 'SK2'),
       ('GPP003', 'Northside Medical Group', 'SK2'),
       ('GPP004', 'Eastgate Surgery', 'SK6'),
       ('GPP005', 'Westview Clinic', 'SK2'),
	     ('GPP006', 'Hillside Family Practice', 'SK3'),
       ('GPP007', 'Park Lane Medical Centre', 'SK2'),
       ('GPP008', 'Lakeside Health Clinic', 'SK3'),
       ('GPP009', 'High Street Surgery', 'SK2'),
       ('GPP100', 'Village Medical Practice', 'SK2'),
       ('GPP011', 'Southern Cross Medical Centre', 'SK2'),
       ('GPP012', 'Riverbank Health Clinic', 'SK5'),
       ('GPP013', 'Springvale Medical Group', 'SK2'),
       ('GPP014', 'Central Square Surgery', 'SK2'),
       ('GPP015', 'Western Avenue Clinic', 'SK9'),
	     ('GPP016', 'Sunrise Medical Centre', 'SK4'),  
       ('GPP017', 'Moorland Health Clinic', 'SK7'),    
       ('GPP018', 'Highland Medical Group', 'SK9'),  
       ('GPP019', 'Coastal Surgery', 'SK5'),       
       ('GPP020', 'City Centre Practice', 'SK2'),      
       ('GPP021', 'Valley View Clinic', 'SK2'),      
       ('GPP022', 'Bridgewater Medical Centre', 'SK4'), 
       ('GPP023', 'Lakeside Health Group', 'SK7'),       
       ('GPP024', 'Market Square Surgery', 'SK2'),      
       ('GPP025', 'Riverside Clinic', 'SK2');

SELECT *
FROM GPPractice;


-- Insert data into GP Table

INSERT INTO GP (GPCode, GPName, GPPracticeCode) VALUES
('GP1', 'Dr. John Smith', 'GPP001'),
('GP2', 'Dr. Emily Johnson', 'GPP002'),
('GP3', 'Dr. Michael Brown', 'GPP003'),
('GP4', 'Dr. Sarah Davis', 'GPP004'),
('GP5', 'Dr. David Wilson', 'GPP005'),
('GP6', 'Dr. Laura Martinez', 'GPP006'),
('GP7', 'Dr. James Anderson', 'GPP007'),
('GP8', 'Dr. Linda Thomas', 'GPP008'),
('GP9', 'Dr. Robert Jackson', 'GPP009'),
('GP10', 'Dr. Patricia White', 'GPP100'),
('GP11', 'Dr. Charles Harris', 'GPP011'),
('GP12', 'Dr. Barbara Clark', 'GPP012'),
('GP13', 'Dr. Christopher Lewis', 'GPP013'),
('GP14', 'Dr. Jennifer Walker', 'GPP014'),
('GP15', 'Dr. Daniel Hall', 'GPP015'),
('GP16', 'Dr. Elizabeth Allen', 'GPP016'),
('GP17', 'Dr. Matthew Young', 'GPP017'),
('GP18', 'Dr. Karen King', 'GPP018'),
('GP19', 'Dr. Richard Wright', 'GPP019'),
('GP20', 'Dr. Susan Scott', 'GPP020'),
('GP21', 'Dr. Joseph Green', 'GPP021'),
('GP22', 'Dr. Margaret Adams', 'GPP022'),
('GP23', 'Dr. Steven Baker', 'GPP023'),
('GP24', 'Dr. Nancy Gonzalez', 'GPP024'),
('GP25', 'Dr. Paul Nelson', 'GPP025'),
('GP26', 'Dr. Amanda Perez', 'GPP001'),
('GP27', 'Dr. Brian Roberts', 'GPP002'),
('GP28', 'Dr. Cynthia Turner', 'GPP003'),
('GP29', 'Dr. Edward Phillips', 'GPP004'),
('GP30', 'Dr. Fiona Campbell', 'GPP005'),
('GP31', 'Dr. George Evans', 'GPP006'),
('GP32', 'Dr. Hannah Mitchell', 'GPP007'),
('GP33', 'Dr. Ian Carter', 'GPP008'),
('GP34', 'Dr. Jessica Collins', 'GPP009'),
('GP35', 'Dr. Kevin Stewart', 'GPP100'),
('GP36', 'Dr. Laura Hughes', 'GPP011'),
('GP37', 'Dr. Mark Richardson', 'GPP012'),
('GP38', 'Dr. Natalie Simmons', 'GPP013'),
('GP39', 'Dr. Oliver Foster', 'GPP014'),
('GP40', 'Dr. Patricia Morgan', 'GPP015'),
('GP41', 'Dr. Quentin Bailey', 'GPP016'),
('GP42', 'Dr. Rachel Cooper', 'GPP017'),
('GP43', 'Dr. Samuel Reed', 'GPP018'),
('GP44', 'Dr. Teresa Murphy', 'GPP019'),
('GP45', 'Dr. Victor Bell', 'GPP020'),
('GP46', 'Dr. Wendy Brooks', 'GPP021'),
('GP47', 'Dr. Xavier Price', 'GPP022'),
('GP48', 'Dr. Yolanda Russell', 'GPP023'),
('GP49', 'Dr. Zachary Bennett', 'GPP024'),
('GP50', 'Dr. Angela Ward', 'GPP025');



-- Insert data into MethodOfAdmission Table

INSERT INTO MethodOfAdmission (MethodOfAdmissionCode, MethodOfAdmissionType)
VALUES ('ELECT', 'Elective'),
       ('EMERG', 'Emergency'),
       ('GP', 'GP'),
       ('NON-ELECT', 'Non-Elective'),
	     ('TRNSFR', 'Transfer'),
       ('PRVT', 'Private'),
       ('MAT', 'Maternity'),
       ('MENT-H', 'Mental Health');

SELECT *
FROM MethodOfAdmission;


-- Insert data into Diagnosis Table

INSERT INTO Diagnosis (DiagnosisCode, DiagnosisDescription)
VALUES('D001', 'Hypertension'),
('D002', 'Diabetes Mellitus Type 1'),
('D003', 'Diabetes Mellitus Type 2'),
('D004', 'Chronic Obstructive Pulmonary Disease'),
('D005', 'Hypertension'),
('D006', 'Asthma'),
('D007', 'Coronary Artery Disease'),
('D008', 'Chronic Kidney Disease'),
('D009', 'Congestive Heart Failure'),
('D010', 'Stroke'),
('D011', 'Liver Cirrhosis'),
('D012', 'Alzheimer''s Disease'),
('D013', 'Parkinson''s Disease'),
('D014', 'Multiple Sclerosis'),
('D015', 'Epilepsy'),
('D016', 'Migraine'),
('D017', 'Osteoarthritis'),
('D018', 'Rheumatoid Arthritis'),
('D019', 'Psoriasis'),
('D020', 'Influenza'),
('D021', 'Pneumonia'),
('D022', 'Tuberculosis'),
('D023', 'HIV/AIDS'),
('D024', 'Malaria'),
('D025', 'Dengue Fever'),
('D026', 'Bronchitis'),
('D027', 'Gastritis'),
('D028', 'Peptic Ulcer Disease'),
('D029', 'Irritable Bowel Syndrome'),
('D030', 'Celiac Disease'),
('D031', 'Crohn''s Disease'),
('D032', 'Ulcerative Colitis'),
('D033', 'Hyperthyroidism'),
('D034', 'Hypothyroidism'),
('D035', 'Anemia'),
('D036', 'Leukemia'),
('D037', 'Lymphoma'),
('D038', 'Melanoma'),
('D039', 'Breast Cancer'),
('D040', 'Prostate Cancer'),
('D041', 'Lung Cancer'),
('D042', 'Colorectal Cancer'),
('D043', 'Pancreatic Cancer'),
('D044', 'Ovarian Cancer'),
('D045', 'Skin Cancer'),
('D046', 'Esophageal Cancer'),
('D047', 'Bladder Cancer'),
('D048', 'Kidney Cancer'),
('D049', 'Thyroid Cancer'),
('D050', 'Cholera'),
('D051', 'Cervical Cancer'),
('D052', 'Testicular Cancer'),
('D053', 'Bone Cancer'),
('D054', 'Sarcoma'),
('D055', 'Liver Cancer'),
('D056', 'Oral Cancer'),
('D057', 'Laryngeal Cancer'),
('D058', 'Nasopharyngeal Cancer'),
('D059', 'Hodgkin''s Lymphoma'),
('D060', 'Non-Hodgkin''s Lymphoma'),
('D061', 'Myeloma'),
('D062', 'Brain Cancer'),
('D063', 'Spinal Cancer'),
('D064', 'Mesothelioma'),
('D065', 'Neuroblastoma'),
('D066', 'Retinoblastoma'),
('D067', 'Wilms'' Tumor'),
('D068', 'Rhabdomyosarcoma'),
('D069', 'Ewing''s Sarcoma'),
('D070', 'Osteosarcoma'),
('D071', 'Chondrosarcoma'),
('D072', 'Germ Cell Tumor'),
('D073', 'Adrenal Cancer'),
('D074', 'Pituitary Tumor'),
('D075', 'Parathyroid Cancer'),
('D076', 'Adrenocortical Carcinoma'),
('D077', 'Pheochromocytoma'),
('D078', 'Merkel Cell Carcinoma'),
('D079', 'Small Cell Lung Cancer'),
('D080', 'Non-Small Cell Lung Cancer'),
('D081', 'Gastrointestinal Stromal Tumor'),
('D082', 'Carcinoid Tumor'),
('D083', 'Medulloblastoma'),
('D084', 'Glioblastoma'), 
('D085', 'Astrocytoma'),
('D086', 'Oligodendroglioma'),
('D087', 'Ependymoma'),
('D088', 'Meningioma'),
('D089', 'Schwannoma'),
('D090', 'Craniopharyngioma'),
('D091', 'Hemangioblastoma'),
('D092', 'Pineal Tumor'),
('D093', 'Chordoma'),
('D094', 'Dermatofibrosarcoma'),
('D095', 'Fibrosarcoma'),
('D096', 'Liposarcoma'),
('D097', 'Angiosarcoma'),
('D098', 'Kaposi''s Sarcoma'),
('D099', 'Synovial Sarcoma'),
('D100', 'Desmoid Tumor'),
('D101', 'Pleomorphic Sarcoma'),
('D102', 'Alveolar Soft Part Sarcoma'),
('D103', 'Clear Cell Sarcoma'),
('D104', 'Epithelioid Sarcoma');

SELECT *
FROM Diagnosis;


-- Insert data into Admission Table

INSERT INTO Admission (PatientID, SpecialtyCode, WardCode, LengthOfStay, AdmissionDate, DischargeDate, MethodOfAdmissionCode, DiagnosisCode, GPPracticeCode) 
VALUES (101, 'CA01', 'ICU', 4, '2015-04-15', '2015-04-19', 'EMERG', 'D050', 'GPP001'), 
(102, 'NE02', 'GEN', 2, '2015-05-23', '2015-05-25', 'GP', 'D002', 'GPP025'), 
(103, 'OR03', 'ENDO', 5, '2014-06-08', '2014-06-13', 'ELECT', 'D003', 'GPP003'), 
(104, 'DE04', 'GEN', 3, '2015-06-10', '2015-06-13', 'EMERG', 'D050', 'GPP004'), 
(105, 'PS05', 'PSYCH', 7, '2015-07-19', '2015-07-26', 'NON-ELECT', 'D050', 'GPP005'), 
(106, 'ON06', 'GEN', 10, '2015-08-01', '2015-08-11', 'GP', 'D006', 'GPP025'), 
(106, 'EN10', 'GEN', 4, '2015-08-18', '2015-08-22', 'GP', 'D007', 'GPP025'), 
(108, 'GE08', 'GEN', 6, '2015-09-20', '2015-09-26', 'EMERG', 'D050', 'GPP008'), 
(109, 'OB09', 'MATERNITY', 2, '2015-10-01', '2015-10-03', 'MAT', 'D009', 'GPP009'), 
(110, 'EN10', 'GEN', 3, '2015-11-07', '2015-11-10', 'GP', 'D010', 'GPP025'), 
(111, 'GA11', 'GAS', 4, '2015-04-07', '2015-04-11', 'GP', 'D011', 'GPP025'), 
(112, 'HE12', 'GEN', 5, '2015-04-10', '2015-04-15', 'EMERG', 'D050', 'GPP012'), 
(113, 'IN13', 'GEN', 8, '2015-04-25', '2015-04-02', 'NON-ELECT', 'D050', 'GPP013'), 
(114, 'NE14', 'NEURO', 6, '2015-04-10', '2015-04-16', 'GP', 'D014', 'GPP025'), 
(115, 'PU15', 'RESP', 10, '2014-05-12', '2014-05-22', 'ELECT', 'D015', 'GPP025'), 
(116, 'RH16', 'GEN', 3, '2015-06-05', '2015-06-08', 'GP', 'D016', 'GPP025'), 
(117, 'SU17', 'ORTHO', 3, '2015-07-03', '2015-07-06', 'GP', 'D017', 'GPP025'), 
(118, 'UR18', 'GEN', 5, '2015-08-14', '2015-08-19', 'NON-ELECT', 'D050', 'GPP018'), 
(119, 'OP19', 'ORTHO', 2, '2015-09-17', '2015-09-19', 'EMERG', 'D019', 'GPP019'), 
(120, 'OT20', 'ORTHO', 3, '2015-10-13', '2015-10-16', 'GP', 'D020', 'GPP025'), 
(121, 'AN21', 'GEN', 2, '2015-11-11', '2015-11-13', 'GP', 'D021', 'GPP025'), 
(122, 'IM22', 'GEN', 4, '2015-12-08', '2015-12-12', 'NON-ELECT', 'D050', 'GPP022'), 
(213, 'FM23', 'GEN', 5, '2016-01-15', '2016-01-20', 'EMERG', 'D023', 'GPP023'), 
(214, 'AI24', 'GEN', 7, '2016-02-23', '2016-03-01', 'GP', 'D024', 'GPP025'), 
(215, 'PR25', 'REHAB', 15, '2016-03-01', '2016-03-16', 'NON-ELECT', 'D050', 'GPP025'),
(216, 'EM26', 'ER', 1, '2016-03-01', '2016-03-02', 'EMERG', 'D050', 'GPP001'), 
(217, 'OP19', 'ORTHO', 4, '2016-03-01', '2016-03-05', 'GP', 'D027', 'GPP025'), 
(218, 'OT20', 'ORTHO', 2, '2016-03-01', '2016-03-03', 'EMERG', 'D050', 'GPP003'), 
(219, 'AN21', 'GEN', 3, '2016-03-01', '2016-03-04', 'GP', 'D029', 'GPP025'), 
(130, 'IM22', 'GEN', 6, '2016-03-01', '2016-03-07', 'NON-ELECT', 'D050', 'GPP005'), 
(131, 'FM23', 'GEN', 5, '2016-03-01', '2016-03-06', 'EMERG', 'D050', 'GPP006'), 
(132, 'AI24', 'GEN', 4, '2016-03-01', '2016-03-05', 'GP', 'D032', 'GPP025'), 
(133, 'PR25', 'REHAB', 20, '2016-01-01', '2016-01-21', 'NON-ELECT', 'D050', 'GPP008'), 
(134, 'GA11', 'GAS', 3, '2015-04-01', '2015-04-04', 'GP', 'D034', 'GPP025'), 
(135, 'NE14', 'GEN', 4, '2015-04-01', '2015-04-05', 'EMERG', 'D050', 'GPP100'), 
(136, 'PU15', 'RESP', 11, '2015-04-01', '2015-04-12', 'GP', 'D036', 'GPP025'), 
(137, 'RH16', 'GEN', 4, '2015-04-01', '2015-04-05', 'GP', 'D037', 'GPP025'), 
(138, 'SU17', 'ORTHO', 4, '2015-05-01', '2015-05-05', 'NON-ELECT', 'D050', 'GPP013'), 
(139, 'UR18', 'GEN', 6, '2015-06-01', '2015-06-07', 'EMERG', 'D050', 'GPP014'), 
(140, 'OP19', 'ORTHO', 1, '2015-07-01', '2015-07-02', 'GP', 'D040', 'GPP025'), 
(141, 'OR03', 'ORTHO', 6, '2015-08-17', '2015-08-23', 'GP', 'D041', 'GPP025'), 
(142, 'HE12', 'GEN', 3, '2015-09-19', '2015-09-22', 'GP', 'D042', 'GPP025'), 
(143, 'IN13', 'GEN', 4, '2015-10-14', '2015-10-18', 'NON-ELECT', 'D050', 'GPP018'), 
(144, 'NE02', 'GEN', 3, '2015-11-11', '2015-11-14', 'EMERG', 'D050', 'GPP019'), 
(145, 'AN21', 'GEN', 2, '2015-12-08', '2015-12-10', 'GP', 'D045', 'GPP025'), 
(146, 'IM22', 'GEN', 4, '2015-04-14', '2015-04-18', 'ELECT', 'D050', 'GPP021'), 
(147, 'FM23', 'GEN', 5, '2015-04-20', '2015-04-25', 'EMERG', 'D050', 'GPP022'), 
(148, 'AI24', 'GEN', 6, '2015-04-14', '2015-04-20', 'GP', 'D048', 'GPP025'), 
(149, 'OR03', 'ORTHO', 10, '2015-04-13', '2015-04-23', 'GP', 'D049', 'GPP024'), 
(150, 'EN10', 'GEN', 3, '2015-05-19', '2015-05-22', 'GP', 'D050', 'GPP025'), 
(151, 'GA11', 'GAS', 4, '2015-06-13', '2015-06-17', 'GP', 'D051', 'GPP025'), 
(152, 'HE12', 'GEN', 3, '2015-07-09', '2015-07-12', 'EMERG', 'D050', 'GPP002'), 
(153, 'IN13', 'GEN', 2, '2015-08-03', '2015-08-05', 'GP', 'D053', 'GPP025'), 
(154, 'NE14', 'NEURO', 8, '2015-09-12', '2015-09-20', 'NON-ELECT', 'D050', 'GPP004'), 
(155, 'PE07', 'PEDS', 5, '2015-10-16', '2015-10-21', 'GP', 'D055', 'GPP025'), 
(156, 'PU15', 'RESP', 14, '2015-11-19', '2015-12-03', 'GP', 'D056', 'GPP025'), 
(157, 'RH16', 'GEN', 7, '2015-12-22', '2015-12-29', 'GP', 'D057', 'GPP025'), 
(158, 'AI24', 'GEN', 6, '2016-01-24', '2016-01-30', 'EMERG', 'D050', 'GPP008'), 
(159, 'AN21', 'GEN', 3, '2016-02-22', '2016-02-25', 'GP', 'D059', 'GPP025'), 
(160, 'IM22', 'GEN', 5, '2016-03-19', '2016-03-24', 'NON-ELECT', 'D050', 'GPP100'), 
(161, 'CA01', 'ICU', 2, '2015-04-05', '2015-04-07', 'GP', 'D061', 'GPP025'), 
(162, 'NE02', 'GEN', 5, '2015-06-15', '2015-06-20', 'NON-ELECT', 'D050', 'GPP002'), 
(163, 'OR03', 'ORTHO', 3, '2015-07-17', '2015-07-20', 'EMERG', 'D050', 'GPP003'), 
(164, 'DE04', 'GEN', 6, '2015-08-14', '2015-08-20', 'GP', 'D064', 'GPP025'), 
(165, 'PS05', 'PSYCH', 8, '2015-10-01', '2015-10-09', 'NON-ELECT', 'D050', 'GPP005'), 
(166, 'ON06', 'GEN', 3, '2015-11-03', '2015-11-06', 'GP', 'D066', 'GPP025'), 
(167, 'PE07', 'PEDS', 2, '2015-12-24', '2015-12-26', 'EMERG', 'D050', 'GPP007'), 
(168, 'GE08', 'GEN', 5, '2015-04-20', '2015-04-25', 'GP', 'D068', 'GPP025'),
(169, 'OB09', 'MATERNITY', 1, '2015-04-07', '2015-04-08', 'MAT', 'D069', 'GPP009'), 
(170, 'EN10', 'GEN', 4, '2015-04-12', '2015-04-16', 'GP', 'D070', 'GPP025'), 
(171, 'GA11', 'GAS', 3, '2015-05-20', '2015-05-23', 'EMERG', 'D050', 'GPP011'),
(172, 'HE12', 'GEN', 2, '2015-06-18', '2015-06-20', 'GP', 'D072', 'GPP025'), 
(173, 'IN13', 'GEN', 5, '2015-07-23', '2015-07-28', 'NON-ELECT', 'D050', 'GPP013'),
(174, 'NE14', 'NEURO', 9, '2015-09-05', '2015-09-14', 'GP', 'D074', 'GPP025'), 
(175, 'PU15', 'RESP', 12, '2015-10-25', '2015-11-06', 'EMERG', 'D050', 'GPP015'), 
(176, 'RH16', 'GEN', 6, '2015-12-08', '2015-12-14', 'GP', 'D076', 'GPP025'), 
(177, 'SU17', 'ORTHO', 4, '2016-01-11', '2016-01-15', 'GP', 'D077', 'GPP025'), 
(178, 'UR18', 'GEN', 5, '2016-02-12', '2016-02-17', 'NON-ELECT', 'D050', 'GPP018'), 
(179, 'OP19', 'ORTHO', 3, '2016-03-18', '2016-03-21', 'EMERG', 'D050', 'GPP019'), 
(180, 'OT20', 'ORTHO', 2, '2016-03-17', '2016-03-19', 'GP', 'D080', 'GPP025'), 
(181, 'CA01', 'ICU', 3, '2015-05-05', '2015-05-08', 'GP', 'D081', 'GPP025'), 
(182, 'NE02', 'GEN', 7, '2015-07-25', '2015-08-01', 'EMERG', 'D050', 'GPP002'), 
(183, 'OR03', 'ORTHO', 4, '2015-08-27', '2015-08-31', 'GP', 'D083', 'GPP025'), 
(184, 'DE04', 'GEN', 2, '2015-09-15', '2015-09-17', 'NON-ELECT', 'D050', 'GPP004'), 
(185, 'PS05', 'PSYCH', 10, '2015-10-30', '2015-11-09', 'GP', 'D085', 'GPP025'), 
(186, 'ON06', 'GEN', 6, '2015-12-13', '2015-12-19', 'GP', 'D086', 'GPP025'), 
(187, 'PE07', 'PEDS', 3, '2015-04-27', '2015-04-30', 'GP', 'D087', 'GPP025'), 
(188, 'GE08', 'GEN', 7, '2015-04-22', '2015-04-01', 'EMERG', 'D050', 'GPP008'), 
(189, 'OB09', 'MATERNITY', 2, '2015-04-10', '2015-04-12', 'MAT', 'D089', 'GPP009'), 
(190, 'EN10', 'GEN', 5, '2015-05-14', '2015-05-19', 'NON-ELECT', 'D050', 'GPP100'), 
(191, 'GA11', 'GAS', 4, '2015-06-16', '2015-06-20', 'GP', 'D091', 'GPP025'), 
(192, 'HE12', 'GEN', 2, '2015-07-25', '2015-07-27', 'GP', 'D092', 'GPP025'), 
(193, 'IN13', 'GEN', 6, '2015-08-21', '2015-08-27', 'GP', 'D093', 'GPP025'), 
(194, 'NE14', 'NEURO', 10, '2015-10-12', '2015-10-22', 'EMERG', 'D050', 'GPP014'), 
(195, 'PU15', 'RESP', 11, '2015-11-25', '2015-12-06', 'GP', 'D095', 'GPP025'), 
(196, 'RH16', 'GEN', 7, '2016-01-28', '2016-02-04', 'NON-ELECT', 'D050', 'GPP016'), 
(197, 'SU17', 'ORTHO', 5, '2016-02-28', '2016-03-04', 'EMERG', 'D050', 'GPP017'), 
(198, 'UR18', 'GEN', 3, '2016-03-28', '2016-03-31', 'GP', 'D098', 'GPP025'), 
(199, 'OP19', 'ORTHO', 6, '2016-03-28', '2016-03-04', 'NON-ELECT', 'D050', 'GPP019'), 
(229, 'OT20', 'ORTHO', 4, '2016-03-28', '2016-03-01', 'GP', 'D050', 'GPP025'), 
(200, 'CA01', 'ICU', 2, '2015-07-02', '2015-07-04', 'GP', 'D001', 'GPP025'), 
(201, 'NE02', 'GEN', 6, '2015-09-20', '2015-09-26', 'EMERG', 'D050', 'GPP002'), 
(202, 'OR03', 'ORTHO', 7, '2015-11-05', '2015-11-12', 'GP', 'D003', 'GPP003'), 
(203, 'DE04', 'GEN', 4, '2015-12-27', '2015-12-31', 'NON-ELECT', 'D050', 'GPP004'), 
(204, 'PS05', 'PSYCH', 8, '2015-04-19', '2015-04-27', 'GP', 'D005', 'GPP025'), 
(205, 'ON06', 'GEN', 10, '2015-04-15', '2015-04-25', 'GP', 'D006', 'GPP025'), 
(206, 'PE07', 'PEDS', 5, '2015-05-18', '2015-05-23', 'GP', 'D007', 'GPP025'), 
(207, 'GE08', 'GEN', 9, '2015-07-02', '2015-07-11', 'EMERG', 'D050', 'GPP008'), 
(208, 'OB09', 'MATERNITY', 4, '2015-08-31', '2015-09-04', 'MAT', 'D009', 'GPP009'), 
(209, 'EN10', 'GEN', 7, '2015-10-06', '2015-10-13', 'NON-ELECT', 'D050', 'GPP100'), 
(210, 'GA11', 'GAS', 6, '2015-11-08', '2015-11-14', 'GP', 'D011', 'GPP011'), 
(211, 'HE12', 'GEN', 4, '2015-12-17', '2015-12-21', 'GP', 'D012', 'GPP025'), 
(220, 'IN13', 'GEN', 8, '2016-02-01', '2016-02-09', 'GP', 'D013', 'GPP025'), 
(221, 'NE14', 'NEURO', 12, '2016-03-19', '2016-03-31', 'EMERG', 'D050', 'GPP014'), 
(222, 'PU15', 'RESP', 9, '2016-03-14', '2016-03-23', 'GP', 'D015', 'GPP025'), 
(223, 'RH16', 'GEN', 9, '2016-03-18', '2016-03-27', 'NON-ELECT', 'D050', 'GPP016'), 
(224, 'SU17', 'ORTHO', 7, '2016-03-28', '2016-03-04', 'EMERG', 'D050', 'GPP017'), 
(225, 'UR18', 'GEN', 5, '2016-03-02', '2016-03-07', 'GP', 'D018', 'GPP025'), 
(226, 'OP19', 'ORTHO', 8, '2016-03-08', '2016-03-16', 'NON-ELECT', 'D050', 'GPP019'),
(227, 'OT20', 'ORTHO', 6, '2016-03-13', '2016-03-19', 'GP', 'D020', 'GPP025'), 
(141, 'CA01', 'ICU', 3, '2015-08-24', '2015-08-27', 'EMERG', 'D050', 'GPP021'),
(142, 'NE02', 'GEN', 5, '2015-04-15', '2015-04-20', 'NON-ELECT', 'D050', 'GPP022'),
(143, 'OR03', 'ORTHO', 6, '2015-04-10', '2015-04-16', 'NON-ELECT', 'D050', 'GPP023'),
(144, 'DE04', 'GEN', 4, '2015-04-05', '2015-04-09', 'EMERG', 'D050', 'GPP024'),
(145, 'PS05', 'PSYCH', 7, '2015-04-18', '2015-04-25', 'EMERG', 'D050', 'GPP025'),
(146, 'ON06', 'GEN', 8, '2015-05-12', '2015-05-20', 'EMERG', 'D050', 'GPP021'),
(147, 'PE07', 'PEDS', 5, '2015-06-22', '2015-06-27', 'NON-ELECT', 'D050', 'GPP021'),
(148, 'GE08', 'GEN', 9, '2015-07-14', '2015-07-23', 'NON-ELECT', 'D050', 'GPP003'),
(149, 'OB09', 'MATERNITY', 4, '2015-08-30', '2015-09-03', 'MAT', 'D099', 'GPP002'),
(150, 'EN10', 'GEN', 7, '2015-09-25', '2015-10-02', 'EMERG', 'D050', 'GPP023'),
(151, 'GA11', 'GAS', 6, '2015-10-18', '2015-10-24', 'EMERG', 'D050', 'GPP001'),
(152, 'HE12', 'GEN', 4, '2015-11-11', '2015-11-15', 'NON-ELECT', 'D050', 'GPP020'),
(153, 'IN13', 'GEN', 8, '2015-12-05', '2015-12-13', 'EMERG', 'D050', 'GPP009'),
(154, 'NE14', 'NEURO', 12, '2015-04-20', '2015-04-01', 'NON-ELECT', 'D050', 'GPP008'),
(155, 'PU15', 'RESP', 9, '2015-04-15', '2015-04-24', 'EMERG', 'D050', 'GPP005'),
(156, 'RH16', 'GEN', 9, '2015-04-10', '2015-04-19', 'EMERG', 'D050', 'GPP006'),
(157, 'SU17', 'ORTHO', 7, '2015-04-05', '2015-04-12', 'NON-ELECT', 'D050', 'GPP007'),
(158, 'UR18', 'GEN', 5, '2015-05-01', '2015-05-06', 'EMERG', 'D050', 'GPP008'),
(159, 'OP19', 'ORTHO', 8, '2015-06-08', '2015-06-16', 'NON-ELECT', 'D050', 'GPP009'),
(160, 'OT20', 'ORTHO', 6, '2015-07-13', '2015-07-19', 'EMERG', 'D050', 'GPP020'),
(161, 'CA01', 'ICU', 3, '2015-08-01', '2015-08-04', 'EMERG', 'D050', 'GPP011'),
(162, 'NE02', 'GEN', 5, '2015-09-10', '2015-09-15', 'NON-ELECT', 'D050', 'GPP012'),
(163, 'OR03', 'ORTHO', 6, '2015-10-05', '2015-10-11', 'NON-ELECT', 'D050', 'GPP013'),
(164, 'DE04', 'GEN', 4, '2015-11-20', '2015-11-24', 'EMERG', 'D050', 'GPP014'),
(165, 'PS05', 'PSYCH', 7, '2015-12-15', '2015-12-22', 'EMERG', 'D050', 'GPP015'),
(166, 'ON06', 'GEN', 8, '2016-01-10', '2016-01-18', 'EMERG', 'D050', 'GPP016'),
(167, 'PE07', 'PEDS', 5, '2016-02-05', '2016-02-10', 'NON-ELECT', 'D050', 'GPP017'),
(168, 'GE08', 'GEN', 9, '2016-03-01', '2016-03-10', 'NON-ELECT', 'D050', 'GPP018'),
(169, 'OB09', 'MATERNITY', 4, '2016-03-15', '2016-03-19', 'MAT', 'D050', 'GPP019'),
(170, 'EN10', 'GEN', 7, '2016-03-10', '2016-03-17', 'EMERG', 'D050', 'GPP020'),
(171, 'GA11', 'GAS', 6, '2016-03-05', '2016-03-11', 'EMERG', 'D050', 'GPP021'),
(172, 'HE12', 'GEN', 4, '2016-03-01', '2016-03-05', 'NON-ELECT', 'D050', 'GPP022'),
(173, 'IN13', 'GEN', 8, '2016-03-10', '2016-03-18', 'EMERG', 'D050', 'GPP023'),
(174, 'NE14', 'NEURO', 12, '2016-03-15', '2016-03-27', 'NON-ELECT', 'D050', 'GPP024'),
(175, 'PU15', 'RESP', 9, '2016-03-10', '2016-03-19', 'EMERG', 'D050', 'GPP025'),
(176, 'RH16', 'GEN', 9, '2016-03-05', '2016-03-14', 'EMERG', 'D050', 'GPP016'),
(177, 'SU17', 'ORTHO', 7, '2016-01-01', '2016-01-08', 'NON-ELECT', 'D050', 'GPP017'),
(178, 'UR18', 'GEN', 5, '2015-04-10', '2015-04-15', 'EMERG', 'D050', 'GPP018'),
(179, 'OP19', 'ORTHO', 8, '2015-04-05', '2015-04-13', 'NON-ELECT', 'D050', 'GPP019'),
(180, 'OT20', 'ORTHO', 6, '2015-04-01', '2015-04-07', 'EMERG', 'D050', 'GPP020'), 
(181, 'CA01', 'ICU', 3, '2015-04-01', '2015-04-04', 'EMERG', 'D050', 'GPP021'),
(182, 'NE02', 'GEN', 5, '2015-05-10', '2015-05-15', 'NON-ELECT', 'D050', 'GPP012'),
(183, 'OR03', 'ORTHO', 6, '2015-06-05', '2015-06-11', 'NON-ELECT', 'D050', 'GPP023'),
(184, 'DE04', 'GEN', 4, '2015-07-20', '2015-07-24', 'EMERG', 'D050', 'GPP024'),
(185, 'PS05', 'PSYCH', 7, '2015-08-15', '2015-08-22', 'EMERG', 'D050', 'GPP025'),
(186, 'ON06', 'GEN', 8, '2015-09-10', '2015-09-18', 'EMERG', 'D050', 'GPP016'),
(187, 'PE07', 'PEDS', 5, '2015-10-05', '2015-10-10', 'NON-ELECT', 'D050', 'GPP017'),
(188, 'GE08', 'GEN', 9, '2015-11-01', '2015-11-10', 'NON-ELECT', 'D050', 'GPP018'),
(189, 'OB09', 'MATERNITY', 4, '2015-12-15', '2015-12-19', 'MAT', 'D050', 'GPP019'),
(190, 'EN10', 'GEN', 7, '2015-04-10', '2015-04-17', 'EMERG', 'D050', 'GPP100'),
(191, 'GA11', 'GAS', 6, '2015-04-05', '2015-04-11', 'EMERG', 'D050', 'GPP011'),
(192, 'HE12', 'GEN', 4, '2015-04-01', '2015-04-05', 'NON-ELECT', 'D050', 'GPP012'),
(193, 'IN13', 'GEN', 8, '2015-04-10', '2015-04-18', 'EMERG', 'D050', 'GPP003'),
(194, 'NE14', 'NEURO', 12, '2015-05-15', '2015-05-27', 'NON-ELECT', 'D050', 'GPP004'),
(195, 'PU15', 'RESP', 9, '2015-06-10', '2015-06-19', 'EMERG', 'D050', 'GPP005'),
(196, 'RH16', 'GEN', 9, '2015-07-05', '2015-07-14', 'EMERG', 'D050', 'GPP006'),
(197, 'SU17', 'ORTHO', 7, '2015-08-01', '2015-08-08', 'NON-ELECT', 'D050', 'GPP007'),
(198, 'UR18', 'GEN', 5, '2015-09-10', '2015-09-15', 'EMERG', 'D050', 'GPP008'),
(199, 'OP19', 'ORTHO', 8, '2015-10-05', '2015-10-13', 'NON-ELECT', 'D050', 'GPP009'),
(200, 'OT20', 'ORTHO', 6, '2015-11-01', '2015-11-07', 'EMERG', 'D050', 'GPP020');

SELECT *
FROM Admission;
```
### Queries and Analysis
1. Patients' details
```sql

SELECT PatientID, 
	CONCAT(Forename,' ', Surname) AS Name,
	Gender,
	DateOfBirth,
	Postcode
FROM Patient;
```
![image](https://github.com/user-attachments/assets/9cc8c6ef-ecc1-488b-b443-c4d89213649c)

This SQL query retrieves the patient IDs, names, gender, date of birth and postcode of all patients. The result includes patient IDs ranging from 101 to 130 and their corresponding details.


2. Patients' total number of admissions
```sql

SELECT P.PatientID, COUNT(A.AdmissionID) AS TotalNumberOfAdmissions
FROM Patient P
LEFT JOIN Admission A ON P.PatientID = A.PatientID
GROUP BY P.PatientID
ORDER BY TotalNumberOfAdmissions DESC;
```
![image](https://github.com/user-attachments/assets/e9b5aac5-2238-4f03-86fa-b862a2fd3290)

This SQL query retrieves all patient IDs and their total number of admissions, e.g., patientID 141 with 2 admissions.


3. Admission analysis
```sql

SELECT A.DischargeDate, 
       W.WardName, 
       M.MethodOfAdmissionType, 
       MAX(A.LengthOfStay) AS MaximumLengthOfStay
FROM Admission A
JOIN Ward W ON A.WardCode = W.WardCode
JOIN MethodOfAdmission M ON A.MethodOfAdmissionCode = M.MethodOfAdmissionCode
WHERE W.WardName = 'Endoscopy Suite' 
  AND M.MethodOfAdmissionType = 'Elective'
  AND A.DischargeDate BETWEEN '2014-04-01' AND '2015-03-31'
GROUP BY A.DischargeDate, W.WardName, M.MethodOfAdmissionType;
```
![image](https://github.com/user-attachments/assets/fff2e2e6-9042-4a7e-81d8-3df02e8b0b57)

This SQL query result shows the maximum length of stay to be 5 days.

4. Total number of admissions for each ward in the financial year 2015/16
```sql

SELECT W.WardCode,
		W.WardName, 
		W.WardType, 
		COUNT(A.AdmissionID) AS TotalNumberOfAdmissions
FROM Ward W
JOIN Admission A ON W.WardCode = A.WardCode
WHERE AdmissionDate BETWEEN '2015-04-01' AND '2016-03-31'
GROUP BY W.WardCode, W.WardName, W.WardType
ORDER BY TotalNumberOfAdmissions DESC;
```
![image](https://github.com/user-attachments/assets/ba3ff41d-c1dc-48e8-9fc6-658d08897800)

This SQL query retrieves all the wards that had admissions in the financial year 2015/16 and their respective number of admissions.

5. Most common diagnosis in the year 2015/16
```sql

SELECT TOP 1 D.DiagnosisCode, 
		D.DiagnosisDescription,
		COUNT(D.DiagnosisCode) AS AdmissionEpisodes
FROM Admission A
JOIN Diagnosis D ON A.DiagnosisCode = D.DiagnosisCode
JOIN MethodOfAdmission M ON A.MethodOfAdmissionCode = M.MethodOfAdmissionCode
JOIN Patient P ON A.PatientID = P.PatientID 
WHERE A.DischargeDate BETWEEN '2015-04-01' AND '2016-03-31'
		AND M.MethodOfAdmissionType ='Emergency'
		AND P.Postcode = 'SK2'
GROUP BY D.DiagnosisCode, D.DiagnosisDescription
ORDER BY AdmissionEpisodes DESC;
```
![image](https://github.com/user-attachments/assets/140c510c-9d7b-4835-9d89-f5b98f0d193f)

This SQL query result shows that Cholera with the Diagnosis code 'D050', is the most common diagnosis, based on the filters applied

6. Primary diagnosis with at least 100 admission episodes
```sql

SELECT TOP 1 
    D.DiagnosisCode,
    D.DiagnosisDescription,
    AVG(A.LengthOfStay) AS AvgLengthofStay,
    COUNT(D.DiagnosisCode) AS AdmissionEpisodes
FROM Admission A
JOIN Diagnosis D ON A.DiagnosisCode = D.DiagnosisCode
JOIN MethodOfAdmission M ON A.MethodOfAdmissionCode = M.MethodOfAdmissionCode
WHERE A.DischargeDate BETWEEN '2015-04-01' AND '2016-03-31'
    AND (M.MethodOfAdmissionType = 'Emergency' 
         OR M.MethodOfAdmissionType = 'Non-Elective')
GROUP BY D.DiagnosisCode, D.DiagnosisDescription
HAVING COUNT(D.DiagnosisCode) > 100
ORDER BY AvgLengthofStay DESC;
```
![image](https://github.com/user-attachments/assets/f0e4dfe7-10ea-4ab0-ab17-0992c640d2b2)

This SQL query result shows that Cholera with the code 'D050' is the primary diagnosis with over 100 admission episodes in the financial year 2015/16, based on the filters applied.


7. GP and Practice analysis 
```sql
SELECT TOP 1 G.GPPracticeCode, 
		G.PracticeName,
		COUNT(A.AdmissionID) AS AdmissionEpisodes
FROM Admission A
JOIN GPPractice G ON A.GPPracticeCode = G.GPPracticeCode
JOIN MethodOfAdmission M ON A.MethodOfAdmissionCode = M.MethodOfAdmissionCode
WHERE AdmissionDate BETWEEN '2015-04-01' AND '2016-03-31'
		AND MethodOfAdmissionType = 'GP'
GROUP BY G.GPPracticeCode, G.PracticeName
ORDER BY AdmissionEpisodes DESC;
```
![image](https://github.com/user-attachments/assets/774b4ebe-995c-406d-91ab-881f5b65099b)

This SQL query shows that Riverside Clinic with the code 'GPP025' has the largest number of hospital admission episodes.


8. Comprehensive Episode Analysis
```sql
-- Generate a list of hospital admission episodes where:
-- (a) The admission date (2nd episode) is within 7 days of a discharge date (1st episode) where the PatientID is the same, but the AdmissionID is different.
-- (b) The admission date of the 2nd episode is after the discharge date of the 1st episode.
-- (c) The method of admission type of the 1st episode is Elective, and the method of admission type of the 2nd episode is Emergency.
-- (d) The specialty code of both admission episodes is the same.
SELECT
    A1.PatientID,
    A1.AdmissionID AS '1st episode AdmissionID',
    A1.DischargeDate AS '1st episode DischargeDate',
	M1.MethodOfAdmissionType AS '1st episode MethodOfAdmissionType',
    A1.SpecialtyCode AS '1st episode SpecialtyCode',
	A2.PatientID,
    A2.AdmissionID AS '2nd episode AdmissionID',
    A2.AdmissionDate AS '2nd episode AdmissionDate',
	M2.MethodOfAdmissionType AS '2nd episode MethodOfAdmissionType',
    A2.SpecialtyCode AS '2nd episode SpecialtyCode',
	DATEDIFF(DAY, A1.DischargeDate, A2.AdmissionDate) AS 'DaysBetweenDischargeAndAdmission'
FROM Admission A1
JOIN Admission A2 ON A1.PatientID = A2.PatientID
JOIN MethodOfAdmission M1 ON A1.MethodOfAdmissionCode = M1.MethodOfAdmissionCode
JOIN MethodOfAdmission M2 ON A2.MethodOfAdmissionCode = M2.MethodOfAdmissionCode
WHERE A1.AdmissionID <> A2.AdmissionID
AND DATEDIFF(DAY, A1.DischargeDate, A2.AdmissionDate) = 7
GROUP BY A1.PatientID, A1.AdmissionID, A1.DischargeDate, M1.MethodOfAdmissionType, A1.SpecialtyCode,
		A2.PatientID, A2.AdmissionID, A2.AdmissionDate, M2.MethodOfAdmissionType, A2.SpecialtyCode
UNION
SELECT
    A1.PatientID,
    A1.AdmissionID AS '1st episode AdmissionID',
    A1.DischargeDate AS '1st episode DischargeDate',
	M1.MethodOfAdmissionType AS '1st episode MethodOfAdmissionType',
    A1.SpecialtyCode AS '1st episode SpecialtyCode',
	A2.PatientID,
    A2.AdmissionID AS '2nd episode AdmissionID',
    A2.AdmissionDate AS '2nd episode AdmissionDate',
	M2.MethodOfAdmissionType AS '2nd episode MethodOfAdmissionType',
    A2.SpecialtyCode AS '2nd episode SpecialtyCode',
	DATEDIFF(DAY, A1.DischargeDate, A2.AdmissionDate) AS 'DaysBetweenDischargeAndAdmission'
FROM Admission A1
JOIN Admission A2 ON A1.PatientID = A2.PatientID
JOIN MethodOfAdmission M1 ON A1.MethodOfAdmissionCode = M1.MethodOfAdmissionCode
JOIN MethodOfAdmission M2 ON A2.MethodOfAdmissionCode = M2.MethodOfAdmissionCode
WHERE A1.AdmissionID <> A2.AdmissionID
AND DATEDIFF(DAY, A1.DischargeDate, A2.AdmissionDate) = 1
GROUP BY A1.PatientID, A1.AdmissionID, A1.DischargeDate, M1.MethodOfAdmissionType, A1.SpecialtyCode,
		A2.PatientID, A2.AdmissionID, A2.AdmissionDate, M2.MethodOfAdmissionType, A2.SpecialtyCode
UNION
SELECT
    A1.PatientID,
    A1.AdmissionID AS '1st episode AdmissionID',
    A1.DischargeDate AS '1st episode DischargeDate',
	M1.MethodOfAdmissionType AS '1st episode MethodOfAdmissionType',
    A1.SpecialtyCode AS '1st episode SpecialtyCode',
	A2.PatientID,
    A2.AdmissionID AS '2nd episode AdmissionID',
    A2.AdmissionDate AS '2nd episode AdmissionDate',
	M2.MethodOfAdmissionType AS '2nd episode MethodOfAdmissionType',
    A2.SpecialtyCode AS '2nd episode SpecialtyCode',
	DATEDIFF(DAY, A1.DischargeDate, A2.AdmissionDate) AS 'DaysBetweenDischargeAndAdmission'
FROM Admission A1
JOIN Admission A2 ON A1.PatientID = A2.PatientID
JOIN MethodOfAdmission M1 ON A1.MethodOfAdmissionCode = M1.MethodOfAdmissionCode
JOIN MethodOfAdmission M2 ON A2.MethodOfAdmissionCode = M2.MethodOfAdmissionCode
WHERE A1.AdmissionID <> A2.AdmissionID
AND M1.MethodOfAdmissionType = 'Elective' 
AND M2.MethodOfAdmissionType = 'Emergency'
GROUP BY A1.PatientID, A1.AdmissionID, A1.DischargeDate, M1.MethodOfAdmissionType, A1.SpecialtyCode,
		A2.PatientID, A2.AdmissionID, A2.AdmissionDate, M2.MethodOfAdmissionType, A2.SpecialtyCode
UNION
SELECT
    A1.PatientID,
    A1.AdmissionID AS '1st episode AdmissionID',
    A1.DischargeDate AS '1st episode DischargeDate',
	M1.MethodOfAdmissionType AS '1st episode MethodOfAdmissionType',
    A1.SpecialtyCode AS '1st episode SpecialtyCode',
	A2.PatientID,
    A2.AdmissionID AS '2nd episode AdmissionID',
    A2.AdmissionDate AS '2nd episode AdmissionDate',
	M2.MethodOfAdmissionType AS '2nd episode MethodOfAdmissionType',
    A2.SpecialtyCode AS '2nd episode SpecialtyCode',
	DATEDIFF(DAY, A1.DischargeDate, A2.AdmissionDate) AS 'DaysBetweenDischargeAndAdmission'
FROM Admission A1
JOIN Admission A2 ON A1.PatientID = A2.PatientID
JOIN MethodOfAdmission M1 ON A1.MethodOfAdmissionCode = M1.MethodOfAdmissionCode
JOIN MethodOfAdmission M2 ON A2.MethodOfAdmissionCode = M2.MethodOfAdmissionCode
WHERE A1.AdmissionID <> A2.AdmissionID
AND A1.SpecialtyCode = A2.SpecialtyCode
GROUP BY A1.PatientID, A1.AdmissionID, A1.DischargeDate, M1.MethodOfAdmissionType, A1.SpecialtyCode,
		A2.PatientID, A2.AdmissionID, A2.AdmissionDate, M2.MethodOfAdmissionType, A2.SpecialtyCode;
```
![image](https://github.com/user-attachments/assets/bae36dcc-37e5-49ea-81c7-7ede14056883)
![image](https://github.com/user-attachments/assets/b9b19cfb-c5d3-44d2-bee4-37c6d67879eb)

This SQL query retrieves all the records that meets the specified criteria above, e.g., The first result shows that PatientID 106 has 2 admission ids(1006 and 1007), and the difference between the first discharge date and the second admission date is 7 days.


9. list of all patients who had more than one admission in the financial year 2015/16
```sql
