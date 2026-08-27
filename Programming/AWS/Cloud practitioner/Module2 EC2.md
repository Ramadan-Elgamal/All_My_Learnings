>**Amazon EC2 (Elastic Compute Cloud) = a virtual server (instance) that runs in the AWS Cloud. The instance type you choose determines the CPU, memory, storage, and network capacity available to it.**

>EC2 is the textbook example of **Infrastructure as a Service (IaaS)**

#### EC2 Sizing & Configuration
- **Operating System (OS):** Choose between Linux, Windows, or macOS.
- **Compute Power & Cores (CPU):** Determine the CPU capacity and number of cores required.
- **Random-Access Memory (RAM):** Specify the amount of RAM needed for optimal performance.
- **Storage Space:**
    - **Network-attached:** Utilize options such as Elastic Block Store (EBS) and Elastic File System (EFS).
    - **Hardware:** Consider storage options provided by EC2 Instance Store.
- **Network Card:** Configure the network card speed and obtain a Public IP address for connectivity.
- **Firewall Rules:** Define security group settings to manage inbound and outbound traffic.
- **Bootstrap Script (Configure at First Launch):** Leverage EC2 User Data to execute scripts or commands during initial setup.

>When you restart your EC2 instance, AWS will change its public ip but the private ip stays the same

>- AWS follows a specific naming convention for its instance types.
    - Example: m6g.2xlarge
        - **m:** instance family (general purpose, compute optimized, etc.)
        - **6:** generation number (AWS improves each family over time higher = newer)
        - **g:** optional attribute, e.g. "g" for AWS Graviton (ARM-based) processor, "n" for network optimized, "d" for local NVMe storage
        - **2xlarge:** size within the instance family (nano → micro → ... → xlarge → 2xlarge → 4xlarge, etc.)

>**The main EC2 instance families the CCP exam expects you to recognize:**
	1. General Purpose (M, T families)
	2. Compute Optimized (C family)
	3. Memory Optimized (R, X families)
	4. Accelerated Computing — GPU/FPGA instances for ML and graphics (P, G, Inf families)
	5. Storage Optimized (I, D, H1 families)

## The 5 Main Categories of EC2 Types:

|**Category**|**What it Focuses On**|**Best Used For**|
|---|---|---|
|**General Purpose (M, T, Mac)**|A balanced mix of CPU, memory, and network speed.|Standard web servers, small databases, and everyday development.|
|**Compute Optimized (C)**|High processing power (CPU).|High-traffic web applications, background automation workflows, and batch processing.|
|**Memory Optimized (R, X)**|Large amounts of RAM.|Big databases (like MySQL or MongoDB) that need to hold a lot of information in memory to stay fast.|
|**Storage Optimized (I, D, H)**|Extremely fast reading and writing to local disks.|Massive data warehouses and systems that log millions of files.|
|**Accelerated Computing (P, G)**|Graphics cards (GPUs) and custom hardware chips.|Machine learning, 3D architectural rendering, and video processing.|

#### **Key AWS tools for right sizing:**
- **AWS Compute Optimizer** the main purpose-built tool; uses machine learning on CloudWatch metrics to recommend optimal EC2, EBS, Lambda, and Auto Scaling Group configurations, flagging resources as over-provisioned, under-provisioned, or optimized.
- **CloudWatch** provides the raw utilization metrics (CPU, network, etc.) right sizing decisions are based on.
- **Cost Explorer** includes rightsizing recommendations focused on cost savings.
- **AWS Trusted Advisor** flags low-utilization EC2 instances as part of its cost optimization checks.

> **Exam tip:** if you see a question about "automated recommendations to resize EC2 instances based on utilization," the answer is **AWS Compute Optimizer**.


>**Quick reference matching purchasing options to scenarios (a favorite CCP exam pattern):**

- "Unpredictable, short-term workload, new project" → **On-Demand**
- "Steady-state production database running 24/7 for the next 3 years" → **Reserved Instance or Savings Plan**
- "Flexible compute spend across EC2, Fargate, and Lambda" → **Compute Savings Plan**
- "Batch job or big-data analysis that can tolerate interruption, cost is the top priority" → **Spot Instance**
- "Must use existing per-core software licenses" → **Dedicated Host**
- "Need guaranteed capacity in an AZ for a product launch, but don't want to fully commit to pricing yet" → **On-Demand Capacity Reservation**

> Security Groups can be attached to **multiple instances and restricted to a specific region and VPC combination a security group created in one VPC cannot be attached to an instance in a different VPC.

>**Security groups are stateful:** if you allow an inbound request, the response traffic is automatically allowed out, regardless of outbound rules you don't need a matching outbound rule.
    - This is a key exam distinction from **Network ACLs (NACLs)**, which are stateless and require explicit rules for both directions.

>**Exam tip:** "security group rules are only allow rules" you cannot create an explicit "deny" rule in a security group (unlike NACLs, which support both allow and deny).

>An EBS (Elastic Block Store) Volume is **a network drive that can be attached to instances while they run.**
>They can be thought of as a **"network USB stick."**

>At the CCP level, think of a standard EBS volume as **attachable to one instance at a time** (the newer io1/io2 Multi-Attach feature is an advanced exception you won't be tested on in depth).

>To move a volume across AZs, you **need to create a snapshot first.**

>Controls the EBS behaviour when **an EC2 instance terminates**
     By default, the root EBS volume is deleted (attribute enabled)
     By default, any other attached EBS volume is not deleted (attribute disabled)

>**Amazon Machine Image (AMI)** = a pre-configured template used to launch an EC2 instance
     Think of it as a "snapshot" of a fully set-up server: OS, installed software, configuration, and monitoring agents, all baked in.

>**EBS volumes are network drives that offer good, but ultimately network-limited, performance.**
   For maximum I/O performance, use **EC2 Instance Store** physically-attached NVMe SSD storage on the underlying host, which delivers much higher IOPS than any network-attached EBS volume.

> **Exam tip:** "ephemeral storage," "highest possible disk I/O," or "data loss on stop" all point to Instance Store. "Persists independently of the instance" points to EBS.

>- Amazon FSx launches and manages **third-party, purpose-built file systems** for specific workloads that EFS/EBS don't natively support.

>- **Exam tip:** you don't need deep FSx internals for the CCP exam just recognize that FSx = "AWS-managed version of a specific, named third-party file system," whereas EFS = "AWS's own native NFS file system."