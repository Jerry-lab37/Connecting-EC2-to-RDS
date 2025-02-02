# Connecting EC2 to RDS: Step-by-Step Guide

## Purpose
This guide provides a step-by-step process to connect an Amazon EC2 instance to an Amazon RDS database. It is useful for developers, system administrators, and cloud engineers who need to set up and manage AWS cloud infrastructure efficiently.

## Step 1: Create an RDS Instance (MySQL or PostgreSQL)
1. Go to **AWS Console → RDS**
2. Click **Create Database**
3. Choose **Standard Create**
4. Select **Engine Type** → MySQL or PostgreSQL
5. Set **DB Instance Identifier** → Example: `my-db-instance`
6. Set **Master Username & Password**
7. Choose **Instance Type** (e.g., `db.t3.micro` for free tier)
8. Enable **Public Access** (Important for EC2 connection)
9. Select **VPC & Security Group** (See Step 3)
10. Click **Create Database**

   _Wait for the RDS instance to become available._

---

## Step 2: Launch an EC2 Instance (Ubuntu/Amazon Linux)
1. Go to **AWS Console → EC2**
2. Click **Launch Instance**
3. Select **Amazon Linux 2** or **Ubuntu**
4. Choose **Instance Type** → `t3.micro` (for free tier)
5. Configure **Security Groups**:
   - Allow **SSH (22)** → Your IP
   - Allow **MySQL (3306)** → From EC2
6. **Key Pair** → Create or select an existing key
7. Click **Launch**

---

## Step 3: Configure Security Group for RDS
1. Go to **AWS Console → EC2 → Security Groups**
2. Find the **Security Group** of your **RDS instance**
3. Click **Inbound Rules → Edit**
4. Allow **MySQL traffic (3306)** from your **EC2 instance's Security Group**
5. Click **Save changes**

---

## Step 4: Connect to EC2 & Install MySQL Client
1. **SSH into your EC2 instance**:
   ```bash
   ssh -i my-key.pem ubuntu@<EC2-PUBLIC-IP>
   ```
2. **Install MySQL Client on EC2**:
   ```bash
   sudo apt update && sudo apt install mysql-client -y
   ```

---

## Step 5: Connect to RDS from EC2
Run the following command on EC2:
```bash
mysql -h my-db-instance.abcdefg.us-east-1.rds.amazonaws.com -u admin -p
```
- Replace `my-db-instance.abcdefg.us-east-1.rds.amazonaws.com` with your **RDS endpoint** (found in the **RDS Console**).
- Enter the password when prompted.

---

## Step 6: Verify Connection
If connected successfully, you should see:
```bash
Welcome to the MySQL monitor...
mysql> SHOW DATABASES;
```

---

## Step 7 (Optional): Test with a Simple Query
Run these SQL commands to test the database:
```sql
CREATE DATABASE testdb;
USE testdb;
CREATE TABLE users (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(100));
INSERT INTO users (name) VALUES ('Alice'), ('Bob');
SELECT * FROM users;
```

---

## Conclusion
You have successfully connected an **EC2 instance** to an **RDS database**. You can now run queries and manage your database remotely.

### 🚀 Happy Cloud Computing!

