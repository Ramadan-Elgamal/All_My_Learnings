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