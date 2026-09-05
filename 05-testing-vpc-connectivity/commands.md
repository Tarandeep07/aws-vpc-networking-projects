# AWS VPC Connectivity — Commands

This file documents the networking commands used during the VPC Connectivity Testing project.

---

## 1. Ping

The `ping` command was used to test connectivity between the public and private EC2 instances.

```bash
ping <PRIVATE_EC2_IP>
```

Replace `<PRIVATE_EC2_IP>` with the private IP address of the destination EC2 instance.

### Purpose

* Test host reachability
* Verify communication between EC2 instances
* Help identify connectivity problems

---

## 2. Curl

The `curl` command was used to test internet connectivity from the public EC2 instance.

```bash
curl example.com
```

### Purpose

* Send an HTTP request to a website
* Verify internet connectivity
* Retrieve the HTTP response from the destination

---

## 3. Connectivity Testing Workflow

The commands were used as part of the following troubleshooting workflow:

```text
Connect to Public EC2
        ↓
ping Private EC2
        ↓
Investigate connectivity failure
        ↓
Review SG / NACL / Route Table
        ↓
ping Private EC2 again
        ↓
curl example.com
```

---

## Security Note

No AWS credentials, access keys, secret keys, passwords, private keys, or other sensitive information are stored in this repository.