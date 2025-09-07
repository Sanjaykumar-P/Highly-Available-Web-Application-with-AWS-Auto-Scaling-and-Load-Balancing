# 🌐 Highly Available Web Application with AWS Auto Scaling and Load Balancing  

## 📖 Project Overview  
This project demonstrates the deployment of a **highly available, scalable, and cost-efficient web application** on AWS using **EC2 instances, an Application Load Balancer (ALB), and an Auto Scaling Group (ASG)**.  
The setup ensures:  
- Real-time traffic distribution ⚖️  
- Automatic scaling 📈  
- Continuous availability 🔐  
- Optimized cloud resource utilization ☁️

- ✨ Key Highlights

Deployed on Amazon EC2 (Linux) with Apache Web Server ☁️

Configured Application Load Balancer for traffic distribution ⚖️

Implemented Auto Scaling Group with scale-in and scale-out policies 📈

Ensured high availability, fault tolerance, and cost optimization 🔐

Strengthened expertise in AWS Cloud, Linux Administration, and Cloud Infrastructure 💻

---

## ❓ What is Auto Scaling Group (ASG)?  
An **Auto Scaling Group (ASG)** automatically manages the number of EC2 instances in your application.  

- **Scale Out**: When traffic or CPU utilization increases (e.g., >70%), ASG launches new EC2 instances.  
- **Scale In**: When traffic decreases, ASG terminates extra instances to reduce costs.  
- **High Availability**: Always keeps minimum instances running to avoid downtime.  

**✨ Benefits:**  
- Ensures scalability during sudden demand  
- Provides fault tolerance and high availability  
- Improves cost efficiency by paying only for used resources  

---

## 🏗️ Architecture  
- **Amazon EC2 (Linux)** → Web servers with Apache HTTPD  
- **Application Load Balancer (ALB)** → Distributes traffic evenly across EC2 instances  
- **Auto Scaling Group (ASG)** → Dynamically scales EC2 instances in/out based on demand  
- **Multiple Availability Zones** → High availability and fault tolerance  

---

## 🛠️ Steps to Implement  

### 1️⃣ Create Target Group  
1. Navigate to **EC2 → Target Groups → Create Target Group**  
2. Target type: **Instances**  
3. Name: `my-target-group`  
4. Protocol: **HTTP**, Port: **80**  
5. VPC: Select your working VPC  
6. Health Checks: Protocol = **HTTP**, Path = `/`  
7. Register EC2 instances → Create  

---

### 2️⃣ Create Application Load Balancer  
1. Navigate to **EC2 → Load Balancers → Create Load Balancer**  
2. Choose **Application Load Balancer**  
3. Configure:  
   - Name: `my-asg-load-balancer`  
   - Scheme: **Internet-facing**  
   - IP Type: **IPv4**  
   - Select VPC + 2 Subnets (for high availability)  
4. Configure Security Group → Allow inbound **HTTP (80)**  
5. Configure Listener → Forward traffic to the Target Group  
6. Review & Create  

---

### 3️⃣ Create Launch Template  
1. Navigate to **EC2 → Launch Templates → Create Template**  
2. Configure:  
   - AMI: **Amazon Linux 2**  
   - Instance Type: `t2.micro` (Free tier eligible)  
   - Security Group: Allow HTTP (80)  
   - User Data Script:  



4️⃣ Create Auto Scaling Group

Navigate to EC2 → Auto Scaling Groups → Create ASG

Select Launch Template created above

Configure VPC + Subnets

Attach to Application Load Balancer Target Group

Configure Desired Capacity:

Min: 2

Desired: 2

Max: 3

Enable ELB Health Checks

Review & Create

5️⃣ Testing the Setup

Copy ALB DNS Name from AWS Console

Example: my-asg-load-balancer-123456.ap-south-1.elb.amazonaws.com

Open in browser → You should see traffic distributed across EC2 instances.

Increase traffic → Observe ASG scale out (new instances launched).

Reduce traffic → Observe ASG scale in (instances terminated).


```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello from $(hostname -f)</h1>" > /var/www/html/index.html
