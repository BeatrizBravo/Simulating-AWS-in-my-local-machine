![LocalStack](https://docs.localstack.cloud/)
Index:
<!-- TOC -->
* [Simulating-AWS-in-my-local-machine](#simulating-aws-in-my-local-machine)
* [AWS](#aws)
* [Simulation](#simulation)
* [LocalStack](#localstack)
* [Requirements](#requirements)
* [Installation](#installation)
* [Try it](#try-it)
<!-- TOC -->

# Simulating-AWS-in-my-local-machine
Install and use localstack



# AWS
The AWS (Amazon Web Services) service is a cloud computing platform that **offers a wide range of services and tools** to help you build and manage applications and services in the cloud . AWS provides services for storage, processing, analytics, artificial intelligence, machine learning, databases, networking, security, and many other aspects of IT infrastructure.
# Simulation

Simulating AWS on your local computer allows you to develop and test applications and services without the need to use real cloud resources. A popular tool for simulating AWS services in your local environment is LocalStack. 

# LocalStack 

LocalStack is an open-source implementation of a local cloud that replicates many of the AWS services. You can use LocalStack to run services like S3, DynamoDB, Lambda, SQS, SNS, and others on your local machine.

Simulating AWS on your local computer can be useful in various situations, such as:

- Development and testing: You can develop and test applications that use AWS services **without incurring cloud costs**. This allows you to iterate quickly and debug your code in a controlled environment.

- Learning: If you are learning to use AWS services, simulating them on your local computer allows you to experiment and familiarize yourself with them **without having to create an AWS account and pay** for the services.

- Isolated environments: You can create isolated environments for development and testing, allowing you to try different configurations and scenarios without impacting your production environment in the cloud.

It is important to note that local simulation is not identical to the real AWS cloud and may have some limitations. However, it can be a useful tool for development and testing in controlled environments.

More Info about LocalStack [here](https://localstack.cloud/). 

# Requirements
- Have  previously installed on your computer:
  - [Installed AWS cl](https://github.com/BeatrizBravo/terraformONE#aws-cli)
  - [docker](https://www.docker.com/get-started/)
- Verify on the console:

```shell
docker version
```
```shell
 aws --version
```

# Installation
- Open docker desktop 
- Open de console and type:

```shell
docker run --rm -it -p 4566:4566 -p 4571:4571 localstack/localstack
```

![Installing LocalStack](https://github.com/BeatrizBravo/Simulating-AWS-in-my-local-machine/blob/main/imagenes/intalling%20LocalStack.PNG)

This command is used to run a Docker container using the localstack/localstack image, with the option to automatically remove the container once its execution is stopped, enable interaction with the container through the terminal, and map the container's ports to the host's ports.
<br><br>
**More details** about the command:
Here is a breakdown of the different components of this command:

**docker run**: This command is used to run a Docker container.<br>
**-it**: These options enable interaction with the container through the terminal. <br>**-i** : option keeps the container's standard input open.<br>**-t** : option allocates a pseudo-terminal.<br>
**-p 4566:4566 -p 4571:4571**: These options map the container's ports to the host's ports. In this case, port 4566 of the container is mapped to port 4566 of the host, and port 4571 of the container is mapped to port 4571 of the host. This allows accessing the services exposed by the container through those ports on the host.<br>
**localsatack/localstack**: This is the name of the container image that will be used to run the container. In this case, the localcatack/localstack image is used.

More Info about LocalStack [here](https://docs.localstack.cloud/getting-started/installation/). 
# Try it

Create a bucket called "mybuckettyt" in the georgraphic area (region)  of Europe (London).

To create this resource you use "Amazon S3" service using the AWS Command Line Interface (CLI) o Terraform. 

 ## Using AWS CLI
Open the console.<br>

```shell
aws --endpoint-url http://localhost:4566 s3api create-bucket --bucket mybuckettyt --region eu-west-2 --create-bucket-configuration LocationConstraint=eu-west-2

```

![creating a resource](https://github.com/BeatrizBravo/Simulating-AWS-in-my-local-machine/blob/main/imagenes/creating%20the%20resorce.PNG)


**_aws_**: This is the command to invoke the AWS CLI.<br><br>
**_--endpoint-url=http://localhost:4566_**: This flag specifies the endpoint URL to which the command should be sent. <br>In this case, it is set to http://localhost:4566, which is the endpoint provided by LocalStack to simulate AWS applications locally.<br><br>

**_s3api_**: This is the service name for Amazon S3 API commands.<br><br>
***create-bucket***: This is the specific command to create a new bucket in Amazon S3.
<br><br>
**_--bucket mybuckettyt_**: This flag specifies the name for the new bucket. You can replace mybuckettyt with your desired bucket name.
<br><br>
_**--region eu-west-2**_: This flag specifies the AWS region in which the bucket should be created. In this example, it is set to eu-west-2, which is the region code for Europe (London).<br><br>
**_--create-bucket-configuration LocationConstraint=eu-west-2_** : This flag configurate the location to London. <br>
In LocalStack to simulate AWS services in your local environment, by default the region "us-east-1" and the endpoint "http://localhost:4566" are compatible and would not need extra configuration. But We want it to point to London, eu-west-2 region. In this case, a LocationConstraint configuration is made pointing to the desired region, which is London.

## Check the list of resources 
Check the list of buckets you have created:
 ```shell
  aws --endpoint-url=http://localhost:4566 s3api list-buckets  
 ```

![List all your buckets](https://github.com/BeatrizBravo/Simulating-AWS-in-my-local-machine/blob/main/imagenes/list%20all%20you%20buckets.PNG)

<br><br>
If you like  more details your can try:
```shell
aws --endpoint-url http://localhost:4566 s3api list-buckets --query "Buckets[*].[Name, CreationDate, LocationConstraint]" --output table

```

![List all your buckets in a table](https://github.com/BeatrizBravo/Simulating-AWS-in-my-local-machine/blob/main/imagenes/list%20all%20you%20buckets%20with%20details.PNG)

<br><br>
In a real AWS environment, the LocationConstraint field would indicate the actual region where the bucket is located. However, since LocalStack is a local simulation of AWS services, it does **not** have the concept of regions and therefore does not provide the region **information**.
<br>The LocationConstraint field will always show "**None**" for buckets listed in LocalStack, regardless of the region specified in the --endpoint-url parameter.