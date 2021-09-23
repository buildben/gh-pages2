---
layout: default
title: Prerequisites
---

# Prerequisites

The executor should have the full admin permissions for the AWS account resources and log in and execute sudo commands on the dedicated `ec2` instance.
Access key to be generated for the executor admin user to be used in `aws-cli` configuration on the `ec2` instance and Jenkins pipeline script.

The following software is to be installed on the `ec2` instance:
* `eksctl`
* `kubectl`
* `helm`

`aws-cli` on `ec2` insurance to be configured with executor admin user credentials.
Appendix A describes in detail the required steps/commands/settings for each requirement.
