CREATE DATABASE PharmaLink;
USE PharmaLink;
CREATE TABLE manufacturers (
    manufacturer_id INT PRIMARY KEY,
    name VARCHAR(100),
    license_no VARCHAR(20),
    country VARCHAR(50),
    contact_email VARCHAR(100)
);
CREATE TABLE medicines (
    medicine_id INT PRIMARY KEY,
    manufacturer_id INT,
    medicine_name VARCHAR(100),
    category VARCHAR(50),
    approval_date DATE,
    FOREIGN KEY (manufacturer_id) REFERENCES manufacturers(manufacturer_id)
);
CREATE TABLE batches (
    batch_id INT PRIMARY KEY,
    medicine_id INT,
    manufacture_date DATE,
    expiry_date DATE,
    quantity INT,
    status VARCHAR(30),
    FOREIGN KEY (medicine_id) REFERENCES medicines(medicine_id)
);
CREATE TABLE pharmacies (
    pharmacy_id INT PRIMARY KEY,
    name VARCHAR(100),
    license_no VARCHAR(20),
    city VARCHAR(50),
    contact_email VARCHAR(100)
);
CREATE TABLE shipments (
    shipment_id INT PRIMARY KEY,
    batch_id INT,
    manufacturer_id INT,
    pharmacy_id INT,
    delivery_date DATE,
    shipment_status VARCHAR(30),
    FOREIGN KEY (batch_id) REFERENCES batches(batch_id),
    FOREIGN KEY (manufacturer_id) REFERENCES manufacturers(manufacturer_id),
    FOREIGN KEY (pharmacy_id) REFERENCES pharmacies(pharmacy_id)
);
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    username VARCHAR(50),
    role VARCHAR(30),
    email VARCHAR(100),
    password_hash VARCHAR(255),
    linked_id INT,
    last_login DATE
);
CREATE ROLE 'admin_role';
CREATE ROLE 'manufacturer_role';
CREATE ROLE 'pharmacist_role';
CREATE ROLE 'auditor_role';
GRANT ALL PRIVILEGES ON PharmaLink.* TO 'admin_role';
GRANT SELECT, UPDATE ON PharmaLink.medicines TO 'manufacturer_role';
GRANT SELECT, UPDATE ON PharmaLink.batches TO 'manufacturer_role';
GRANT SELECT, UPDATE ON PharmaLink.shipments TO 'manufacturer_role';
GRANT SELECT ON PharmaLink.shipments TO 'pharmacist_role';
GRANT SELECT ON PharmaLink.pharmacies TO 'pharmacist_role';
GRANT SELECT ON PharmaLink.medicines TO 'pharmacist_role';
CREATE USER 'admin_user'@'%' IDENTIFIED BY 'Admin@123';
GRANT 'admin_role' TO 'admin_user';
CREATE USER 'manu_user'@'%' IDENTIFIED BY 'Manu@786';
GRANT 'manufacturer_role' TO 'manu_user';
CREATE USER 'pharma_user'@'%' IDENTIFIED BY 'Pharma@420';
GRANT 'pharmacist_role' TO 'pharma_user';
CREATE USER 'audit_user'@'%' IDENTIFIED BY 'Audit@777';
GRANT 'auditor_role' TO 'audit_user';
SET DEFAULT ROLE ALL TO 
'admin_user', 
'manu_user', 
'pharma_user', 
'audit_user';
-- Added Encrypted Coloumns
ALTER TABLE manufacturers
ADD COLUMN enc_license_no BLOB,
ADD COLUMN enc_contact_email BLOB;
ALTER TABLE pharmacies
ADD COLUMN enc_license_no BLOB,
ADD COLUMN enc_contact_email BLOB;
ALTER TABLE users
ADD COLUMN enc_password_hash BLOB;
-- Encrypt manufacturer data
UPDATE manufacturers
SET enc_license_no = AES_ENCRYPT(license_no, 'PLSL_Key_2025'),
    enc_contact_email = AES_ENCRYPT(contact_email, 'PLSL_Key_2025');
-- Encrypt pharmacy data
UPDATE pharmacies
SET enc_license_no = AES_ENCRYPT(license_no, 'PLSL_Key_2025'),
    enc_contact_email = AES_ENCRYPT(contact_email, 'PLSL_Key_2025');
-- Encrypt user password hashes
UPDATE users
SET enc_password_hash = AES_ENCRYPT(password_hash, 'PLSL_Key_2025');
-- Admin Full Decryption
CREATE OR REPLACE VIEW admin_manufacturers_view AS
SELECT 
    manufacturer_id,
    name,
    AES_DECRYPT(enc_license_no, 'PLSL_Key_2025') AS license_no,
    AES_DECRYPT(enc_contact_email, 'PLSL_Key_2025') AS contact_email,
    country
FROM manufacturers;
-- Auditor No Decryption (encrypted columns hidden)
CREATE OR REPLACE VIEW auditor_manufacturers_view AS
SELECT 
    manufacturer_id,
    name,
    country
FROM manufacturers;
-- Users Table – Encrypted Passwords
ALTER TABLE users
ADD COLUMN enc_password_hash BLOB;
UPDATE users
SET enc_password_hash = AES_ENCRYPT(password_hash, 'PLSL_Key_2025');
CREATE OR REPLACE VIEW admin_users_view AS
SELECT
    user_id,
    username,
    role,
    AES_DECRYPT(enc_password_hash, 'PLSL_Key_2025') AS password_hash
FROM users;
CREATE OR REPLACE VIEW auditor_users_view AS
SELECT
    user_id,
    username,
    role
FROM users;
-- Admin full access
GRANT SELECT ON PharmaLink.admin_pharmacies_view TO 'admin_user'@'%';
-- Pharmacist limited access
GRANT SELECT ON PharmaLink.pharmacist_pharmacies_view TO 'pharma_user'@'%';
-- Auditor minimal access
GRANT SELECT ON PharmaLink.auditor_pharmacies_view TO 'audit_user'@'%';
-- Admin can view decrypted passwords (for demonstration)
GRANT SELECT ON PharmaLink.admin_users_view TO 'admin_user'@'%';
-- Auditor can only see usernames and roles
GRANT SELECT ON PharmaLink.auditor_users_view TO 'audit_user'@'%';
-- Updated View
CREATE OR REPLACE VIEW admin_users_view AS
SELECT
    user_id,
    username,
    role,
    CAST(AES_DECRYPT(enc_password_hash, 'PLSL_Key_2025') AS CHAR(100)) AS password_hash
FROM users;
CREATE OR REPLACE VIEW admin_pharmacies_view AS
SELECT
    pharmacy_id,
    name,
    CAST(AES_DECRYPT(enc_license_no, 'PLSL_Key_2025') AS CHAR(50)) AS license_no,
    CAST(AES_DECRYPT(enc_contact_email, 'PLSL_Key_2025') AS CHAR(100)) AS contact_email,
    city
FROM pharmacies;
CREATE OR REPLACE VIEW admin_pharmacies_view AS
SELECT
    pharmacy_id,
    name,
    CAST(AES_DECRYPT(enc_license_no, 'PLSL_Key_2025') AS CHAR(50)) AS license_no,
    CAST(AES_DECRYPT(enc_contact_email, 'PLSL_Key_2025') AS CHAR(100)) AS contact_email,
    city
FROM pharmacies;
CREATE OR REPLACE VIEW pharmacist_pharmacies_view AS
SELECT
    pharmacy_id,
    name,
    CAST(AES_DECRYPT(enc_license_no, 'PLSL_Key_2025') AS CHAR(50)) AS license_no,
    city
FROM pharmacies;
CREATE OR REPLACE VIEW admin_manufacturers_view AS
SELECT 
    manufacturer_id,
    name,
    CAST(AES_DECRYPT(enc_license_no, 'PLSL_Key_2025') AS CHAR(50)) AS license_no,
    CAST(AES_DECRYPT(enc_contact_email, 'PLSL_Key_2025') AS CHAR(100)) AS contact_email,
    country
FROM manufacturers;
CREATE OR REPLACE VIEW manufacturer_manufacturers_view AS
SELECT 
    manufacturer_id,
    name,
    CAST(AES_DECRYPT(enc_license_no, 'PLSL_Key_2025') AS CHAR(50)) AS license_no,
    country
FROM manufacturers;
CREATE OR REPLACE VIEW auditor_manufacturers_view AS
SELECT 
    manufacturer_id,
    name,
    country
FROM manufacturers;
-- Drop Plaintext Columns
ALTER TABLE manufacturers
DROP COLUMN license_no,
DROP COLUMN contact_email;
ALTER TABLE pharmacies
DROP COLUMN license_no,
DROP COLUMN contact_email;
ALTER TABLE users
DROP COLUMN password_hash;
DESC manufacturers;
DESC pharmacies;
DESC users;
-- Data Integrity
ALTER TABLE medicines ADD COLUMN data_hash VARCHAR(64);
UPDATE medicines
SET data_hash = SHA2(CONCAT(medicine_name, manufacturer_id), 256);
SELECT 
    medicine_id,
    medicine_name,
    data_hash,
    SHA2(CONCAT(medicine_name, manufacturer_id), 256) AS current_hash,
    CASE 
        WHEN data_hash = SHA2(CONCAT(medicine_name, manufacturer_id), 256) 
        THEN 'VALID' 
        ELSE 'TAMPERED'
    END AS integrity_status
FROM medicines;
