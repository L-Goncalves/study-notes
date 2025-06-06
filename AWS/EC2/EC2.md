## Amazon EC2

* EC2 is one of the most popular of AWS' offering
* ES2 means Elastic Compute Cloud = Infrastructure as a Service.
* It mainly consists in the capability of:
  * Renting virtual machines (EC2)
  * Storing data on virtual drives (EBS)
  * Distributing load across machines (ELB)
  * Scalling the services using an auto-scalling group (ASG)

### EC2 Sizing & Configuration Options:

* Operating System (OS): Linux, Windows or Mac OS
* How much compute power & cores (CPU)
* How much random access memory ( RAM)
* How much storage:

  * Network-Attached (EBS & EFS)
  * Hardware EC2 Instance Store
* Network Card: speed of the card, Public IP Address
* Firewall Rules: security group
* Bootstrap Script (Configure at first launch): EC2 User Data

### EC2 User Data:

* It is possible to bootstrap our instances using an EC2 User Data Script
* Bootstrapping means launching commands when a machine starts
* That Script is only run once at the instance first start
* EC2 user data is used to automate boot tasks such as:
  * Installing Updates
  * Installing software
  * Downloading common files from the internet
  * Anything you can think of
* Any command run has the SUDO permissions

### EC2 Instance Types:

| Instance    | vCPU | Memory (GiB) | Storage           | Network Performance | EBS Bandwidth (Mbps) |
| ----------- | ---- | ------------ | ----------------- | ------------------- | -------------------- |
| t2.micro    | 1    | 1            | EBS-Only          | Low to Moderate     | -                    |
| t2.xlarge   | 4    | 16           | EBS-Only          | Moderate            | -                    |
| c5d.4xlarge | 16   | 32           | 1 × 400 NVMe SSD | Up to 10 Gbps       | 4,750                |
| r5.16xlarge | 64   | 512          | EBS-Only          | 20 Gbps             | 13,600               |
| m5.8xlarge  | 32   | 128          | EBS-Only          | 10 Gbps             | 6,800                |

* t2.micro is part of AWS free tier (up to 750 hours per month)

#### Creating a new instance:

From the home click on launch new instances, it will make you go into a new page of EC2, there you can configure what you want.

The current free tier as of this date (09/05/2025) [DD/MM/YYYY] is t2.micro

##### SSH

* We need:
* Key-pair name
* Key-pair type
* Private Key format

To SSH we need a new key pair with RSA and save as:

.ppk is used in lower versions of Windows like Windows 7

.pem is the most common.

##### Storage

* Free tier gets me 30GB of EBS General Purpose

#### Important

After creating an instance on AWS make sure to check the IP address on the internet to check availability.

* If HTTPs is not marked only http requests will be accepted
* The public IPV4 can change if stopped and start again.

#### Terminating Instance

It's like deleting forever the instance.

* The Instance store volumes are lost
* The data on EBS Volumes:
  * If the EBS volume is **root** and has the `DeleteOnTermination` flag = true (default), it is  **deleted** .
  * If it’s an attached EBS volume without `DeleteOnTermination`, the volume **remains** and you are charged for it.
* Security Groups, key pairs AMIs and snapshots remain. They're not deleted
