---
layout: post
title: "AWS Networking Basics"
date: 2024-06-08
description: "With AWS CDK Examples"
giscus_comments: true
toc:
  sidebar: left
tags: co
---

AWS Networking is complex. The [AWS Networking and Content Delivery page](https://aws.amazon.com/products/networking/) lists 19 products grouped into 5 categories. As with so much of AWS, it can be hard to navigate.

## VPC

You have a default VPC

## CIDR Ranges

CIDR classless

Private IP address ranges

IPv4 /16 to /28

IPv6 /56

10.0.0.0        -   10.255.255.255  (10/8 prefix)
     172.16.0.0      -   172.31.255.255  (172.16/12 prefix)
     192.168.0.0     -   192.168.255.255 (192.168/16 prefix)

Conflicting IP address ranges should be avoided

RFC1918 https://datatracker.ietf.org/doc/html/rfc1918

## Subnet

Each AWS region has availability zones

Availability zones are separate risk domains

You need a subnet for each availability zone

Can have multiple subnets in an AZ

Public subnet instances have private and public IP address

Has a route to an internet gateway

Private subnet instance only have private IP address

### Elastic IP

Static IPv4 address designed for dynamic cloud computing

Dynamically assigned

Can be associated with an instance or network interface

Can be remapped to another instance in your account

## Connecting to the Internet

### Internet Gateway

2-way connection point between VPC and internet

1 per VPC

### NAT gateway

NAT service

1-way connection point that allows outbound network traffic

Can NAT between subnets

## Route Table

Each subnet has a route table

Route tables contain rules for which packets go where

You VPC



| Destination | Target |
| ----------- | ------ |
| /8          | Local  |
| 0.0.0.0/0   | igw_id |



| Destination | Target    |
| ----------- | --------- |
| /8          | Local     |
| 0.0.0.0/0   | nat_gw_id |



## Network Security

### Security Groups

Distributed firewall

Operates at instance level

Supports allow rules only

Automatically allows return traffic to requests

### Network Access Control List

Operates at subnet level

Supports allow and deny rules

Doesn't automatically allow return traffic to requests

Should be used sparingly

### VPC Flow Logs

Record format

Interface source IP destination IP source port destination port bytes condition



## Connecting VPCs

### VPC Peering

Connects source VPC with destination VPC

Doesn't automatically connect all subnets

Routing is done through route tables

### Transit Gateway

Connects multiple VPCs in the same region

Allows routing

### VPC Sharing

Subnets in VPC can be shared with another AWS account

## VPC Endpoints

### Gateway VPC Endpoints

Used to reach Amazon S3 and DynamoDb from within your VPC

### Interface VPC Endpoints

Used to reach other AWS services from within your VPC

Appears as if the service is within your VPC

AWS PrivateLink

Can be used to share your service with other VPCs

They connect to a local IP address that goes to your VPC endpoint
