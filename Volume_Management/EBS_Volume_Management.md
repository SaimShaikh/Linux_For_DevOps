# AWS EBS Volume Management on Linux

This guide explains how to **create**, **attach**, **format**, **mount**, and **move** an Amazon **EBS Volume** between EC2 instances running Amazon Linux.

---

## 1. Prerequisites
- AWS account
- At least **two EC2 instances** running Amazon Linux (in the **same Availability Zone** as your EBS volume)
- IAM permissions for EC2 & EBS operations
- SSH access to both EC2 instances

---

## 2. Step-by-Step Procedure

### **Step 1 — Create EBS Volume**
1. Open **AWS Management Console → EC2 → Volumes → Create Volume**.
2. Choose:
   - **Size**: 10 GB  
   - **Availability Zone**: Same as your EC2 instance  
   - **Volume Type**: gp3 (or gp2)  
3. Click **Create Volume**.

---

### **Step 2 — Attach Volume to EC2**
1. Select your newly created volume.
2. Click **Actions → Attach Volume**.
3. Choose the target EC2 instance.
4. Note the **device name** AWS assigns (e.g., `/dev/sdf`).

---

### **Step 3 — Identify Volume in EC2**
SSH into the EC2 instance:
```bash
ssh -i mykey.pem ec2-user@<EC2_PUBLIC_IP>
