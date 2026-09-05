# AWS CLI Commands — Project 1

This file contains the AWS CLI commands used while building and managing the
VPC environment.

## 1. Create a VPC

```bash
aws ec2 create-vpc --cidr-block 10.0.0.0/16 --query Vpc.VpcId --output text
```

## 2. Naming VPC

```bash
aws ec2 create-tags --resources=VPC-ID --tags Key=Name,Value="my-vpc-01"
```

## 3. Subnet Creation

```bash
aws ec2 create-subnet --vpc-id VPC-ID --cidr-block 10.0.0.0/24
```

## 4. Creating Internet Gateway for VPC

```bash
aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text
```

## 5. Attaching Internet Gateway to VPC

```bash
aws ec2 attach-internet-gateway --vpc-id VPC-ID --internet-gateway-id IG-ID
```

## 6. Create a Route Table

```bash
aws ec2 create-route-table --vpc-id VPC-ID
```

## 7. Create an Internet Route

```bash
aws ec2 create-route --route-table-id ROUTE-TABLE-ID --destination-cidr-block 0.0.0.0/0 --gateway-id IGW-ID
```

## 8. Associate the Route Table with the Subnet

```bash
aws ec2 associate-route-table --route-table-id ROUTE-TABLE-ID --subnet-id SUBNET-ID
```