---
title: "Cloud One - File Storage Security"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 4.1.2. </b> "
---


## File Storage Security

File Storage Security is part of the Trend Micro Cloud One™ security service platform, helping your organization to build and run applications securely by offering controls that work across your existing infrastructure or modern code streams, development toolchains, and multiplatform requirements. File Storage Security helps ensure your Amazon S3 buckets are free from malware by deploying cloud-native security that can be integrated into your custom Amazon S3 workflows.

File Storage Security is backed by Trend Micro Research, which continuously monitors and collects threat data from across the globe by employing advanced detection analytics to immediately block attacks before they can harm your organization.

## Understanding How Trend Micro Can Help Secure Your Object Storage

There are two main ways to use File Storage Security in your AWS Infrastructure:

* **File Upload Scan**: Any cloud-native application that uses the power of the cloud to provide features integrated with Amazon S3 buckets could be exposed to malware. File Storage Security allows customers to integrate scan capabilities directly to their AWS accounts, so all of the files you receive in your Amazon S3 buckets from external sources can be scanned for malware before your application can consume the data.
* **Automated Workflow**: Development teams leverage event-driven designs with Amazon S3 to automate the processing of data uploaded to a bucket. File Storage Security was designed with this architecture in mind allowing development teams to seamlessly integrate file scanning into their automated workflow.
* **S3 bucket Full Scan or Scheduled Scan**: Helps security teams to scan all the objects inside AWS S3 buckets against malicious contents. [GitHub link for Plugin](#) 

## Architecture

Cloud-native application architectures incorporate cloud file/object storage services into their workflow, creating a new attack vector where they are vulnerable to malicious files. File Storage Security protects the workflow through innovative techniques, such as malware scanning, integration into your custom workflows, and broad cloud storage platform support – freeing you to go further and do more. File Storage Security provides flexible implementation options, including a multi-bucket promotional model (scanning bucket to quarantine/clean bucket) or an efficient single-bucket architecture.
![fss](/images/5-Workshop/5.1-Workshop-overview/fss.png)
File Storage Security’s architecture was built to be simple to understand and monitor all of the buckets. As soon as a new file is uploaded to the bucket, this will generate a SQS message inside your AWS account that will trigger an AWS Lambda function. The function will execute the scan and tag the file as malicious or clean, depending on the scan result. It is also possible to connect plugins to perform additional actions, for example, as soon the file is tagged as malicious, the plugin moves the tagged file to a quarantine bucket.

Digging a little deeper into the architecture details, the overall deployment is made up of two different stacks:

* **Storage Stack**: This stack is responsible for accepting the notification for the Amazon S3 bucket, as well as sending newly uploaded files to the Scanner Stack for the security scan. After the scan is complete, an Amazon SNS topic is published and the file is tagged as “malicious” or “clean”—additional plugins are available to add more functionality to the stack.
* **Scanner Stack**: This stack is responsible for executing the scan and publishing the results to the Amazon SNS ScanResultTopic. When the Scanner Stack receives the request from the Storage Stack, its processes it and uses an AWS Lambda function to execute the scan. Like many Trend Micro technologies, File Storage Security can leverage Trend Micro™ Smart Protection Network™ for the latest threat information.
![fss_archi](/images/5-Workshop/5.1-Workshop-overview/fss_architecture.png)
## File Scanning Information

The file hash is sent to Trend Micro Global Smart Scan Server when a file scan occurs and enables File Storage Security to identify malicious file hashes.

In the smart scan solution, clients send file hashes determined by Trend Micro technology to Smart Scan Servers. **Cloud One - File Storage Security never sends the entire file** and the risk of the file is determined using the file hashes.
