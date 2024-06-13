---
title: StableDiffusion on AWS
info: How to create a personal generative AI server with AWS
credits: based on the "Stable Diffusion Art" post available at https://stable-diffusion-art.com/aws-ec2/
pub date: 2024-06-11, 10:59
tags:
  - varia
---

> [!warning]
> **!!! WORK IN PROGRESS AND NOT FULLY TESTED !!!**

## 01 Create a new EC2 instance

1. Log in to AWS. In the top search bar, type “EC2”. Click the **EC2** service.
2. Click **lanch instance**.
3. In the "Launch Instance" page, use these settings:
	-  **Name**: you choose it
	- **Amazon Machine Image**: Ubuntu Server 24.04 LTS
	- **Instance type**: g4dn.xlarge
4.  Next, create a security key pair. In **Key pair (login)**, click **Create new key pair**. Give it a name and click **create pair**. The pem key file should be downloaded automatically.
5. In **Configure Storage**, change the storage to 100 GiB.
6. Click **Launch instance**.
7. If Service Quota problems occur, check [this link](https://console.aws.amazon.com/servicequotas/home/services/ec2/quotas/) to upgrade the EC2 service quota. 
---

## 02 SetUp the EC2 Instance

1.  Open the [Amazon EC2 console](https://console.aws.amazon.com/ec2). Select **Instances** in the sidebar. You should see your instance initializing. The machine is ready to use when the **Status check** changes to checks passed. Select the EC2 instance and click **Connect**. In the **EC2 Instance Connect**, ensure the Username is *ubuntu* and click **Connect**. You should now have access to the machine’s terminal. Alternatively, you can ssh the machine from your local PC using the information in the **SSH client** tab.
2.  Run these commands:
```bash
   sudo apt update
```
```bash
   sudo apt upgrade
```
```bash
   sudo apt install nvidia-driver-535
```
```bash
   sudo add-apt-repository ppa:deadsnakes/ppa
```
```bash
   sudo apt install python3.10
```
```bash
   sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.10 2
```
```bash
   python3 --version
```
```bash
   sudo apt install python3.10-venv
```
3. Restart the instance by using the AWS interface. *Instance state > Reboot instance.* When the reboot is complete, and the instance is ready, start a new terminal and confirm that the NVidia driver is working with:
```bash
   nvidia-smi
```

---