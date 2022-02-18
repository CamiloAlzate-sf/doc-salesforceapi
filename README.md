# Managing Salesforce API versions
An overview of what the Salesforce Legacy API update entails, as well as best practices on identifying versions and upgrading. 

- [Introduction](#introduction)
- [Identifying API calls on deprecated versions](#identifying-api-calls-on-deprecated-versions)
- [Updating Legacy API calls](#updating-legacy-api-calls)

## Introduction

This document will be a reference guide for maintaining our Salesforce API versions.

With each 'Summer Update', Salesforce retires old versions of the API, stops support for other versions and announces the next set of versions that are set for retirement in the next update. A call to a retired API will just return an error, which can potentially break multiple organizational processes.

Fortunately, there are multiple resources that we can use in order to readily identify applications doing API calls using a deprecated version. With this information, we can then proceed to update the API version in our REST, SOAP and Bulk endpoint URLs accordingly.

## Identifying API calls on deprecated versions

There are multiple ways to do this. But some of the most comprehensive and easy to use ways are listed here:

1. By reviewing event logs that report SOAP and REST API activity, examining the Bulk Data Load Jobs for the Bulk API, and reviewing the Login History on SOAP() login operations we can identify if there's any versions used that are soon to be deprecated. The step-by-step guide is outline on this [Salesforce Help Center](https://help.salesforce.com/s/articleView?id=000351312&type=1) article.

While useful, the instructions provided in the Salesforce Blog and lengthy and can take some time to properly review. We can also take a look at a couple of open source solutions that facilitate this process:

2. There's a simple script called [sfdc-goodbye-api](https://github.com/pgonzaleznetwork/sfdc-goodbye-api) which identifies REST and SOAP API calls under a version threshold and then logs the restults in CSV files for better perusal.
3. [sfdx-hardis](https://hardisgroupcom.github.io/sfdx-hardis/) is a tool provided by the Hardis Group Salesforce Team has a very useful command to detect Legacy API usage. Further details on how to use this command with this tool can be found on their [blog post](https://nicolas.vuillamy.fr/handle-salesforce-api-versions-deprecation-like-a-pro-335065f52238).

## Updating Legacy API calls

After properly identifying the applications that are doing API calls using a deprecated, or soon to be retired version, we can proceed and update the API version in the endpoint URLs used, depending on the API used. For example:

### **REST API**
```
From
https://staffingcompany.salesforce.com/services/data/v18.0/users/User

To
https://staffingcompany.salesforce.com/services/data/v30.0/users/User
```

### **SOAP API**
```
From
https://staffingcompany.salesforce.com/services/soap/c/v18.0

To
https://staffingcompany.salesforce.com/services/soap/c/v30.0
```

### **Bulk API**
```
From
https://staffingcompany.salesforce.com/services/async/c/v18.0/job

To
https://staffingcompany.salesforce.com/services/async/c/v30.0/job
```
