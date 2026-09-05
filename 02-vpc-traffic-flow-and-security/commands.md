# AWS CLI Commands — Project 2

This file contains the AWS CLI commands used while building and managing the
VPC environment.

## 1. Create a VPC

```bash
aws ec2 create-vpc --cidr-block 10.0.0.0/16 --query Vpc.VpcId --output text --tag-specifications "ResourceType=vpc, Tags=[{Key=Name,Value=vpc01}]"
```

## 2. Subnet Creation

```bash
aws ec2 create-subnet --vpc-id VPC-ID --cidr-block 10.0.0.0/24
```

## 3. Creating Internet Gateway for VPC

```bash
aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text
```

## 4. Attaching Internet Gateway to VPC

```bash
aws ec2 attach-internet-gateway --vpc-id VPC-ID --internet-gateway-id IG-ID
```
## 5. Creating Security Group

```bash
aws ec2 create-security-group --query "GroupId" --output text --description "New SG Created" --group-name security-group-vpc-01 --tag-specifications "ResourceType=security-group,Tags=[{Key=vpc01,Value=sg01}]"
```

## 6. Creating rule for Security Group - Inbound Rule

```bash
aws ec2 authorize-security-group-ingress --group-id GROUP-ID --ip-permissions "IpProtocol=tcp,FromPort=80,ToPort=80,IpRanges=[{CidrIp=0.0.0.0/0,Description='Security Group rule created for inbound traffic'}]"
```

## 7. Creating rule for Security Group - Outbound Rule

```bash
aws ec2 authorize-security-group-egress --group-id GROUP-ID --ip-permissions IpProtocol=-1,IpRanges='[{CidrIp=0.0.0.0/0}]'
```

## 8. Create a Route Table

```bash
aws ec2 create-route-table --vpc-id VPC-ID
```

## 9. Create an Internet Route

```bash
aws ec2 create-route --route-table-id ROUTE-TABLE-ID --destination-cidr-block 0.0.0.0/0 --gateway-id IGW-ID
```

## 10. Associate the Route Table with the Subnet

```bash
aws ec2 associate-route-table --route-table-id ROUTE-TABLE-ID --subnet-id SUBNET-ID
```

## 11. Creating Network ACL

```bash
aws ec2 create-network-acl --vpc-id VPC-ID --tag-specifications "ResourceType=network-acl,Tags=[{Key=Name,Value=vpc01_acl}]"
```

## 12. Creating rule for Network ACL - Inbound Rule

```bash
aws ec2 create-network-acl-entry --network-acl-id ACL-ID --rule-number 100 --protocol tcp --port-range From=80,To=80 --cidr-block 0.0.0.0/0 --rule-action allow --ingress
```

## 13. Creating rule for Network ACL - Outbound Rule

```bash
aws ec2 create-network-acl-entry --network-acl-id ACL-ID --rule-number 100 --protocol tcp --port-range From=80,To=80 --cidr-block 0.0.0.0/0 --rule-action allow --egress
```