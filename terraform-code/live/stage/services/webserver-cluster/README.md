# Creating webservers cluster and load balancer in AWS using terraform module
This folder contains terraform code that pulls code form module folder and it creates webservers cluster and load balancer in AWS. Make sure to create MySQL databse first because webservers cluster depends on it. 


--------------------------------------------------------------------------------------------------------------
### List of files in this folder:
- main.tf - terraform configuration file that pulls code form module that creates webserver cluster and load balancer.
- variables.tf - terraform configuration file with input variables.
- output.tf - terraform configuration file with output parameters.
----------------------------------------------------------------------------------------------------------------------
### How to use this part of the repository:
- install `terraform` from [here](https://www.terraform.io/downloads.html).
- setup Amazon Web Services (AWS) account [here](https://aws.amazon.com/).
- configure your AWS access keys [here](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys).
- configure your AWS access keys as environment variables so you can authenticate to your AWS account:

```
export AWS_ACCESS_KEY_ID="your access key id here"
export AWS_SECRET_ACCESS_KEY="your secret access key here"
```
   
- clone the repository to your local computer: `git clone https://github.com/nikcbg/TF_Book_Ch_5`.
- go into the cloned repo on your computer: `cd TF_Book_Ch_5`.
- go into the subfolder which is this example `cd loops-and-if-statements/live/prod/services/webserver-cluster`.

------------------------------------------------------------------------------------------------------------------

### Configure remote state using S3 bucket:
- terraform state file of this folder will be using the module state file which uses MySQL state file stored in the S3 bucket 
- add the below code to your `variables.tf` file:
   - both `default` parameters don't have to be uploaded to GitHub, they can exist only in your code in your local computer.

```
variable "db_remote_state_bucket" {
  description = "The name of the S3 bucket used for the database's remote state storage"
  default = "name-of-your-S3-bucket"
}

variable "db_remote_state_key" {
  description = "The name of the key in the S3 bucket used for the database's remote state storage"
  default = "path to the state file inside the bucket"
}
```

-------------------------------------------------------------------------------------------------------------------

### Commands needed to build the webservers cluster and laod balancer.
- execute `terraform init` - to initialize the provider and download the neccesery plugins.
  
- execute `terraform plan` - to create execution plan for changes to be applied, the output should diplay the following:

```
Terraform will perform the following actions:

+ aws_security_group_rule.allow_testing_inbound
+ module.webserver_cluster.aws_autoscaling_group.example
+ module.webserver_cluster.aws_cloudwatch_metric_alarm.high_cpu_utilization
+ module.webserver_cluster.aws_cloudwatch_metric_alarm.low_cpu_credit_balance
+ module.webserver_cluster.aws_elb.example
+ module.webserver_cluster.aws_launch_configuration.example
+ module.webserver_cluster.aws_security_group.elb
+ module.webserver_cluster.aws_security_group.instance
+ module.webserver_cluster.aws_security_group_rule.allow_all_outbound
+ module.webserver_cluster.aws_security_group_rule.allow_http_inbound
+ module.webserver_cluster.aws_security_group_rule.allow_server_http_inbound

Plan: 11 to add, 0 to change, 0 to destroy.
```
  
- execute `terraform apply` - to apply the desired changes, the output should diplay the following:

```
Terraform will perform the following actions:

module.webserver_cluster.aws_security_group.elb: Creation complete after 6s (ID: sg-01762c67bd93c840e)
module.webserver_cluster.aws_security_group.instance: Creation complete after 6s (ID: sg-0059adf6550885907)
module.webserver_cluster.aws_security_group_rule.allow_all_outbound: Creation complete after 2s (ID: sgrule-4267303657)
module.webserver_cluster.aws_security_group_rule.allow_server_http_inbound: Creation complete after 2s (ID: sgrule-2804614377)
module.webserver_cluster.aws_launch_configuration.example: Creation complete after 2s (ID: terraform-20190228115657391900000001)
aws_security_group_rule.allow_testing_inbound: Creation complete after 5s (ID: sgrule-199468075)
module.webserver_cluster.aws_security_group_rule.allow_http_inbound: Creation complete after 8s (ID: sgrule-803633740)
module.webserver_cluster.aws_elb.example: Creation complete after 11s (ID: webservers-stage)
module.webserver_cluster.aws_autoscaling_group.example: Creation complete after 3m35s (ID: webservers-stage-terraform-20190228115657391900000001)
module.webserver_cluster.aws_cloudwatch_metric_alarm.low_cpu_credit_balance: Creation complete after 2s (ID: webservers-stage-low-cpu-credit-balance)
module.webserver_cluster.aws_cloudwatch_metric_alarm.high_cpu_utilization: Creation complete after 2s (ID: webservers-stage-high-cpu-utilization)

Apply complete! Resources: 11 added, 0 changed, 0 destroyed.

Outputs:

elb_dns_name = name-of-webserver-cluster
```
- execute `terraform destroy` - to destroy the resources you created, the output should diplay the following:
  
```
module.webserver_cluster.aws_security_group_rule.allow_server_http_inbound: Destruction complete after 1s
module.webserver_cluster.aws_cloudwatch_metric_alarm.low_cpu_credit_balance: Destruction complete after 1s
module.webserver_cluster.aws_cloudwatch_metric_alarm.high_cpu_utilization: Destruction complete after 1s
module.webserver_cluster.aws_security_group_rule.allow_all_outbound: Destruction complete after 2s
aws_security_group_rule.allow_testing_inbound: Destruction complete after 3s
module.webserver_cluster.aws_security_group_rule.allow_http_inbound: Destruction complete after 5s
module.webserver_cluster.aws_autoscaling_group.example: Destruction complete after 1m58s
module.webserver_cluster.aws_launch_configuration.example: Destruction complete after 1s
module.webserver_cluster.aws_elb.example: Destruction complete after 3s
module.webserver_cluster.aws_security_group.instance: Destruction complete after 2s
module.webserver_cluster.aws_security_group.elb: Destruction complete after 2m2s

Destroy complete! Resources: 11 destroyed.
```
