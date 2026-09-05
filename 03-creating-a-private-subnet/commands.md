# AWS CLI Commands — Project 3

This file contains the AWS CLI commands used while creating and managing the VPC environment for the private subnet project.

## 1. Describing a VPC

```bash
aws ec2 describe-vpcs --vpc-ids VPC-ID
```

## 2. Describing a Subnet

```bash
aws ec2 describe-subnets --filters Name=vpc-id,Values=VPC-ID
```

## 3. Creating a Private Subnet

```bash
aws ec2 create-subnet --vpc-id VPC-ID --cidr-block 10.0.1.0/24 --tag-specifications "ResourceType=subnet,Tags=[{Key=Name,Value=private1}]"
```

## 4. Creating a Private Route Table

```bash
aws ec2 create-route-table --vpc-id VPC-ID
```

## 5. Naming the Private Route Table

```bash
aws ec2 create-tags --resources ROUTE-TABLE-ID --tags "Key=Name,Value=private_route_01"
```

## 6. Associating the Route Table with the Private Subnet

```bash
aws ec2 associate-route-table --route-table-id ROUTE-TABLE-ID --subnet-id SUBNET-ID
```

## 7. Creating a Private Network ACL

```bash
aws ec2 create-network-acl --vpc-id VPC-ID --tag-specifications "ResourceType=network-acl,Tags=[{Key=Name,Value=private_nacl_01}]"
```

## 8. Associating the Private Network ACL with the Private Subnet

First, retrieve the Network ACL association ID for the private subnet:

```bash
aws ec2 describe-network-acls --filters "Name=association.subnet-id,Values=SUBNET-ID" --query "NetworkAcls[].Associations[?SubnetId=='SUBNET-ID'].NetworkAclAssociationId" --output text
```

Then replace the existing association with the newly created private Network ACL:

```bash
aws ec2 replace-network-acl-association --association-id ASSOCIATION-ID --network-acl-id NETWORK-ACL-ID
```

## 9. Network ACL Inbound and Outbound Rules

Since the default rules of a newly created custom Network ACL deny both inbound and outbound traffic, no additional deny rules are required for this project.

The custom Network ACL therefore remains configured with its default deny rules for both inbound and outbound traffic.
