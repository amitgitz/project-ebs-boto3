# Event-Driven Architecture for maintaing companies policy for only using EBS volume 'gp3' using LambdaFunction and CloudWatch and IAM !
Created a lambda script using boto3 to convert EBS volume gp2 to gp3 automatically.

# Project Application
Suppose you work in a company which only works with the gp3 ebs but by mistake someone created the EBS with gp2 in that scenario it will convert the gp2 to gp3 automatically

# AWS Lambda Setup
  - Login to the AWS Account
  - Create a lambda function named `ebs-volume-check`
  ![image](https://github.com/amitgitz/project-ebs-boto3/assets/88843810/8ccf2050-a8ea-4146-9940-94125accfe5c)

  - Run the test
 # CloudWatch Setup
  - Rules
     1. Event Source : Event Pattern
     2. Service Name : EC2
     3. Event Type : EBS Volument Notification
     4. Specific Event : create volume
     5. Target : Lambda Function
     6. Function : ebs-volume-check
     7. Name : ebs-vol-check

  # Event Pattern 
  ```
   {
    "source": ["aws.ec2"],
    "detail-type": ["EBS Volume Notification"],
    "detail": {
      "event": ["createVolume"]
    }
  }
  ```

![image](https://github.com/amitgitz/project-ebs-boto3/assets/88843810/d25eea91-0036-46a8-824b-fc401dd9b072)

# IAM Setup
Roles -> Permission Policies -> ebs-vol-check

![image](https://github.com/amitgitz/project-ebs-boto3/assets/88843810/233ffdc8-9bcc-43f5-b749-209751cd49d3)
Click on `Add permission` -> `Create inline policity` 
  - Service : EC2
  - Actions : Volume
        - Create Volume 
        - Modify Volume
        - Modify Volume Attribute
        - Describe Volumes
        - Describe Volumes Attribute

    - Resources : All resources

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "ec2:ModifyVolume",
                "ec2:ModifyVolumeAttribute",
                "ec2:CreateVolume"
            ],
            "Resource": "*"
        }
    ]
}
```
![image](https://github.com/amitgitz/project-ebs-boto3/assets/88843810/0d0c0579-d35c-4958-9045-9a2a236eafd4)


# Create a gp2 volume and test the function
  - Created volume with gp2
  ![image](https://github.com/amitgitz/project-ebs-boto3/assets/88843810/6c5ad225-dc00-4f04-9411-b3cb3cb22fe2)  
  - Automatically changed to gp3
  ![image](https://github.com/amitgitz/project-ebs-boto3/assets/88843810/2876d664-1f14-4a09-b1b2-24aa074604ec)

  
  Congratulations! Your ebs has been changed to gp3
 - If you have any questions or encounter any problems with this project, feel free to connect with me on https://www.linkedin.com/in/devopsamit/

  








