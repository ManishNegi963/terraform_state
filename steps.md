# Local State

- To show the list of resource in state file

      terraform state list

<img width="478" alt="image" src="https://github.com/ManishNegi963/terraform_state/assets/124788172/3cb4ebb9-a330-43d4-b781-99da6fe84b80">

terraform generate the state file after the use of command terraform apply, as it store the state of the resource created in the terraform.tfstate file in form object 
for example resource "aws_instance" "my_demo_instance is the object  and if we store that file locally it's called loval state or if remotely its called remote state.

- To show the attribute in the object of resource stored in terraform.tfstate fie

      terraform state show aws_s3_bucket.my_bucket

  <img width="636" alt="image" src="https://github.com/ManishNegi963/terraform_state/assets/124788172/473efa79-f1ab-46ed-8a68-c03b4a7dd1a7">

arn, bucket, region, etc. are called attributes of objects in the state file and they are called arguments while they are in the configuration file. 

NOTE: Once the arguments provision using the command terraform apply they are called attributes.

# Remote state

NOTE:
Suppose Person A is using the terraform.tfstate remote on S3 bucket to  create infrastructure and another person B is also creating the infrastructure using the same bucket,
When person A does some changes to the infrastructure it will change the tfstate file and person B also make some changes and it will also change the tfstate file which will lead to conflict 
to resolve this we will create a dynamodb table with the infrastructure which will make an entry while a person make changes to the infrastructure and does changes to the tfstate file and
for the time till person A does changes to the infrastructure, the person B will get the message as person A has locked the state file  and till the lock dynamodb table will be active and person B would not be able to process his changes to the statefile. This concept is known as state locking in terraform. 

State locking is the measure we take to prevent the state from being changed by any other teammate.

