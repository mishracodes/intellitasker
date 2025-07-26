
# 📦 IntelliTasker Infrastructure Setup (Day 1–4)

This document outlines the complete AWS infrastructure setup for IntelliTasker from Day 1 to Day 4, designed to be cost-effective while covering critical networking and compute fundamentals.

---

## ✅ Day 1: GitHub Project Setup

1. **Created GitHub Repository**: `intellitasker`
2. **Initialized Branching Strategy**:
   - `main` → production-ready code
   - `dev` → ongoing development
   - `feature/*` → short-lived feature branches
3. **Folder Structure**:
   ```
   intellitasker/
   ├── backend/
   ├── frontend/
   ├── infrastructure/
   ├── README.md
   ├── .gitignore
   └── LICENSE
   ```
4. **First Commit**:
   - `.gitignore` for Python
   - `README.md` with project vision
   - `LICENSE` (MIT)

---

## ✅ Day 2: VPC and Networking (Free-Tier Optimized)

1. **VPC Created**: `intellitasker-vpc` with CIDR `10.0.0.0/16`
2. **Subnets Created**:
   - `public-subnet-a` (10.0.1.0/24, AZ-a)
   - `public-subnet-b` (10.0.2.0/24, AZ-b)
   - `private-subnet-a` (10.0.3.0/24, AZ-a)
   - `private-subnet-b` (10.0.4.0/24, AZ-b)
3. **Internet Gateway (IGW)**:
   - Created and attached to the VPC
   - Public route table updated with `0.0.0.0/0 → IGW`
4. **Private subnets kept isolated** (no NAT Gateway yet to reduce cost)

---

## ✅ Day 3: Bastion Host EC2 Setup

1. **Created Key Pair**: `intellitasker-key.pem` (downloaded & chmod 400)
2. **Security Group**: `bastion-sg`
   - Inbound: SSH (22) from `My IP`
3. **EC2 Launched**:
   - Name: `intellitasker-bastion`
   - AMI: Amazon Linux 2
   - Type: `t2.micro` (Free Tier)
   - Subnet: `public-subnet-a`
   - Public IP: Enabled
4. **SSH Verified**:
   ```bash
   ssh -i "intellitasker-key.pem" ec2-user@<Public-IP>
   ```

---

## ✅ Day 4: Private EC2 + Bastion SSH Tunnel

1. **Security Group**: `private-ec2-sg`
   - Inbound SSH (22) allowed **only from `bastion-sg`**
2. **EC2 Launched**:
   - Name: `intellitasker-app-ec2`
   - Subnet: `private-subnet-a`
   - Key Pair: `intellitasker-key.pem`
   - No public IP assigned
3. **SSH via Bastion**:
   ```bash
   # From local to Bastion
   ssh -i "intellitasker-key.pem" ec2-user@<Bastion_Public_IP>

   # From Bastion to Private EC2
   chmod 400 intellitasker-key.pem
   ssh -i intellitasker-key.pem ec2-user@<Private_IP>
   ```
4. **Result**: Fully functional, secure jump-host SSH architecture without NAT Gateway.

---

✅ You are now ready to proceed with **Day 5: RDS Setup in Private Subnet**
