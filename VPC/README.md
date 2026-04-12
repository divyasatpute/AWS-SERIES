# 🌐 AWS VPC Setup – Step-by-Step Guide

This document explains how to create a Virtual Private Cloud (VPC) in AWS with public and private subnets, routing, and internet access.

---

## 📌 Step 1: Create VPC

1. Go to AWS Console → VPC  
2. Click on **Create VPC**  
3. Select **VPC only**  
4. Enter:
   - Name: `My-VPC`
   - IPv4 CIDR: `10.0.0.0/16`
   - Tenancy: Default  
5. Click **Create VPC**

---

## 📌 Step 2: Create Subnets

We will create:
- Public Subnet
- Private Subnet

---

### 🌍 Public Subnet

1. Go to **Subnets**  
2. Click **Create Subnet**  
3. Select your VPC  
4. Enter:
   - Name: `Public-Subnet`
   - Availability Zone: Any  
   - IPv4 CIDR: `10.0.0.0/24`  
5. Click **Create**

---

### 🔒 Private Subnet

1. Go to **Subnets**  
2. Click **Create Subnet**  
3. Select your VPC  
4. Enter:
   - Name: `Private-Subnet`
   - Availability Zone: Different from public subnet  
   - IPv4 CIDR: `10.0.1.0/24`  
5. Click **Create**

---

## 📌 Step 3: Create Internet Gateway (IGW)

1. Go to **Internet Gateways**  
2. Click **Create Internet Gateway**  
3. Enter Name: `My-IGW`  
4. Click **Create**

---

## 📌 Step 4: Attach IGW to VPC

1. Select the IGW  
2. Click **Actions → Attach to VPC**  
3. Select your VPC  
4. Click **Save**

---

## 📌 Step 5: Create Route Table (Public)

1. Go to **Route Tables**  
2. Click **Create Route Table**  
3. Enter:
   - Name: `Public-RT`
   - Select your VPC  
4. Click **Create**

---

## 📌 Step 6: Add Route for Public Access

1. Select `Public-RT`  
2. Go to **Routes → Edit Routes**  
3. Add:
   - Destination: `0.0.0.0/0`
   - Target: Internet Gateway (IGW)  
4. Save

---

## 📌 Step 7: Associate Public Subnet

1. Go to **Subnet Associations**  
2. Click **Edit**  
3. Select **Public Subnet**  
4. Save

---

## 📌 Step 8: Create Route Table (Private)

1. Go to **Route Tables**  
2. Click **Create Route Table**  
3. Enter:
   - Name: `Private-RT`
   - Select your VPC  
4. Click **Create**

---

## 📌 Step 9: Create NAT Gateway

1. Go to **NAT Gateways**  
2. Click **Create NAT Gateway**  
3. Select:
   - Public Subnet  
   - Allocate Elastic IP  
4. Click **Create**

---

## 📌 Step 10: Add Route for Private Subnet

1. Select `Private-RT`  
2. Go to **Routes → Edit Routes**  
3. Add:
   - Destination: `0.0.0.0/0`
   - Target: NAT Gateway  
4. Save

---

## 📌 Step 11: Associate Private Subnet

1. Go to **Subnet Associations**  
2. Click **Edit**  
3. Select **Private Subnet**  
4. Save

---

## 📌 Step 12: Network ACL (Optional)

- AWS automatically creates NACL  
- Used to control inbound and outbound traffic  

---


## 📌 Step 13: Create NAT Gateway (For Private Subnet Internet Access)

A **NAT Gateway** allows instances in the **private subnet** to access the internet securely (without exposing them publicly).

---

### 🔧 Steps to Create NAT Gateway

1. Go to **NAT Gateways** section in AWS Console  
2. Click on **Create NAT Gateway**

3. Configure:
   - **Subnet**: Select **Public Subnet**
   - **Elastic IP**: Click **Allocate Elastic IP**

---

### 💡 Important Note

- Elastic IP acts as a **static public IP**
- Unlike normal EC2 public IPs, it **does not change**
- Required for NAT Gateway to communicate with the internet

---

### 🔁 Configure Routing for Private Subnet

1. Go to **Route Tables**
2. Select **Private Route Table**
3. Click on **Routes → Edit Routes**
4. Add:
   - Destination: `0.0.0.0/0`
   - Target: **NAT Gateway**
5. Click **Save**

---

### 🔗 Associate Private Subnet

1. Go to **Subnet Associations**
2. Click **Edit**
3. Select **Private Subnet**
4. Click **Save**

---

## ✅ Result

- Private instances can now access:
  - Internet (for updates, packages, etc.)
- But they are **not directly accessible from outside** 🔒
## ✅ Architecture Summary

- VPC CIDR: `10.0.0.0/16`  
- Public Subnet → Internet access via IGW  
- Private Subnet → Internet access via NAT Gateway  
- Secure and scalable network setup  

---

## 🚀 Bonus Tip

- Public Subnet → Load Balancer / Bastion Host  
- Private Subnet → Application / Database  

---

Also watch My Youtube Video Do Like, share, Subscribe
https://youtu.be/k7XdtwNsBHQ?si=g22If2I5BBiI4zCS

<img width="600" height="600" alt="AWS series (1)" src="https://github.com/user-attachments/assets/ae3bd58c-5f13-4e09-93fb-770a6c3eaa45" />


<img width="1536" height="1024" alt="AWS VPC architecture diagram" src="https://github.com/user-attachments/assets/4ec62125-2e5c-45a5-a021-c1d231dffc98" />


## 💡 Author

**Divya Satpute (Teacode 1122)**  
Helping beginners learn DevOps in a simple way ❤️
