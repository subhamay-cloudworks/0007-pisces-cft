# Project Pisces: AWS S3 Cross Account / Cross Region Replication


## Description

This sample project demonstrate the S3 bucket cross region and cross account replication. Three S3 buckets are created in two regions in Account-A and one bucket in third region in Account-B. All the three buckets are encrypted with KMS Customer Managed Keys. Once an object is uploaded to the bucket in the primary region, the same is replicated in the other two buckets with storage class as Standard IA (in second region is Account-A) and as Glacier Instant Retrieval (in third region in Account-B). The entire stack is created AWS CloudFormation.

![Project Pisces - Design Diagram](https://subhamay-projects-repository-us-east-1.s3.amazonaws.com/0007-pisces/pisces-architecture-diagram.png?)

![Project Pisces - Services Used](https://subhamay-projects-repository-us-east-1.s3.amazonaws.com/0007-pisces/pisces-services-used.png?)


### Dependencies

* You need to have two AWS Accounts to implement this.
* Create three Customer Managed KMS Keys in the regions where you want to create the stack. First two in Account-A and the third one in Account-B
* Modify the KMS Key Policy to let the AWS Account (root) encrypt / decrypt using any resource using the created KMS Key. In the destination account KMS Key policy, grant permission to source account to use the key for S3 bucket.

### Installing

* Clone the repository.
* Create a S3 bucket as code repository to store the CF templates.
* Create the folders - pisces/cft
* Upload the following YAML templates to pisces/cft
    * s3-stack-template.yaml
    * pisces-stack-set.yaml
*  Setup AWS CloudFormation Stack Set Administration Role and AWS CloudFormation Stack Set Execution Role in Account-A.
    * Log in to Account-A
    * Create CloudFormation Stack Set Administration Role in both the source and destination accounts using the CF Template https://s3.amazonaws.com/cloudformation-stackset-sample-templates-us-east-1/AWSCloudFormationStackSetAdministrationRole.yml
    * Create CloudFormation Stack Set Execution Role in both the source and destination accounts using the CF Template https://s3.amazonaws.com/cloudformation-stackset-sample-templates-us-east-1/AWSCloudFormationStackSetExecutionRole.yml. Pass the Administration Account Id (the Account Id of Account -A)
*  Setup AWS CloudFormation Stack Set Administration Role and AWS CloudFormation Stack Set Execution Role in Account-B.
    * Log in to Account-B
    * Create CloudFormation Stack Set Administration Role in both the source and destination accounts using the CF Template https://s3.amazonaws.com/cloudformation-stackset-sample-templates-us-east-1/AWSCloudFormationStackSetAdministrationRole.yml
    * Create CloudFormation Stack Set Execution Role in both the source and destination accounts using the CF Template https://s3.amazonaws.com/cloudformation-stackset-sample-templates-us-east-1/AWSCloudFormationStackSetExecutionRole.yml. Pass the Administration Account Id (the Account Id of Account -A)
* Create the S3 buckets in all the three regions in two AWS Accounts by logging into Account A and running the stackset template.
    * Go to CloudFormation -> StackSets and create the Create Stackset
    ![Project Pisces - Create StackSet](https://subhamay-projects-repository-us-east-1.s3.amazonaws.com/0007-pisces/pisces-creating-stack-set.png?)
    * Provide the values of the required parameters.
    ![Project Pisces - StackSet Parameters](https://subhamay-projects-repository-us-east-1.s3.amazonaws.com/0007-pisces/pisces-creating-stack-set-parameters.png?)
    * Provide the Administration AccountId and Region.
    ![Project Pisces - StackSet Administration Account](https://subhamay-projects-repository-us-east-1.s3.amazonaws.com/0007-pisces/pisces-creating-stack-set-adm-account.png?)
* Click create stack to create the entire stack.

### Executing program

* Upload the sample sample file to the S3 bucket in Region-1 in Account-A
* Within a few seconds (depending on the size) the object will be replicated to all the three regions.
![Project Pisces - S3 Cross Region Replication](https://subhamay-projects-repository-us-east-1.s3.amazonaws.com/0007-pisces/pisces-s3-cross-region-replication.png?)

## Help

Post message in my blog (https://blog.subhamay.com)


## Authors

Contributors names and contact info

Subhamay Bhattacharyya  - [subhamay.aws@gmail.com](https://blog.subhamay.com)

## Version History

* 0.1
    * Initial Release

## License

This project is licensed under Subhamay Bhattacharyya. All Rights Reserved.

## Acknowledgments

Inspiration, code snippets, etc.
* [Stephane Maarek ](https://www.linkedin.com/in/stephanemaarek/)
* [Neal Davis](https://www.linkedin.com/in/nealkdavis/)
* [Adrian Cantrill](https://www.linkedin.com/in/adriancantrill/)
