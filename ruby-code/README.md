# Ruby automated test for webservers cluster

Ruby automated test for webservers cluster which will apply Terraform code and then it will test if the webservers cluster returns "Hello World" and then destroy the webservers cluster. 

---------------------------------------------------------------------------------------------------------------------------
### Pre-requisites for running the Ruby script:
-install `ruby` from [here](https://www.ruby-lang.org/en/)
- install `terraform` from [here](https://www.terraform.io/downloads.html).
- setup Amazon Web Services (AWS) account [here](https://aws.amazon.com/).
- configure your AWS access keys [here](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys).
- configure your AWS access keys as environment variables so you can authenticate to your AWS account:

```
export AWS_ACCESS_KEY_ID="your access key id here"
export AWS_SECRET_ACCESS_KEY="your secret access key here"
```
- clone the repository to your local computer: `git clone https://github.com/nikcbg/TF_Book_Ch_6`.
- go into the cloned repo on your computer: `cd TF_Book_Ch_6`.
- go into the subfolder which is this example `cd ruby-code`.

-------------------------------------------------------------------------------------------------------------------------
### Steps needed to run the Ruby script:
- deploy database that the webserver cluster can connect, you can use the follwoing database:
  - [terraform-code/live/stage/data-stores/mysql](https://github.com/nikcbg/TF_Book_Ch_6/tree/master/terraform-code/live/stage/data-stores/mysql) to deploy MySQL database.
- next go to a folder that contains web servers cluster configuration code, you can use the following code:
  - [terraform-code/live/stage/services/webserver-cluster](https://github.com/nikcbg/TF_Book_Ch_6/tree/master/terraform-code/live/stage/services/webserver-cluster) to run ruby automated test.
- make sure the database and the webservers cluster are using the same S3 bucket and key to store their state files.
- next execute the following command in webserver-cluster folder to run the ruby scrip:
  - `ruby /path/to/your/ruby/script/ruby-code/terraform-test.rb us-east-1 tfstate-file-bucket terraform.tfstate`
  - the output should display teh following:
```
  Plan: 11 to add, 0 to change, 0 to destroy.
  
  module.webserver_cluster.aws_security_group.instance: Creation complete after 4s (ID: sg-022285e2a6ddbb600)
  module.webserver_cluster.aws_security_group.elb: Creation complete after 5s (ID: sg-09cf55f5d84bf10db)
  module.webserver_cluster.aws_launch_configuration.example: Creation complete after 2s (ID: terraform-20190308093025464700000001)
  module.webserver_cluster.aws_security_group_rule.allow_server_http_inbound: Creation complete after 2s (ID: sgrule-1618770031)
  module.webserver_cluster.aws_security_group_rule.allow_http_inbound: Creation complete after 2s (ID: sgrule-3367295172)
  module.webserver_cluster.aws_security_group_rule.allow_all_outbound: Creation complete after 4s (ID: sgrule-51411494)
  aws_security_group_rule.allow_testing_inbound: Creation complete after 6s (ID: sgrule-1045364580)
  module.webserver_cluster.aws_elb.example: Creation complete after 10s (ID: GRSFBR)
  module.webserver_cluster.aws_autoscaling_group.example: Creation complete after 3m37s (ID: GRSFBR-terraform-20190308093025464700000001)
  module.webserver_cluster.aws_cloudwatch_metric_alarm.high_cpu_utilization: Creation complete after 1s (ID: GRSFBR-high-cpu-utilization)
 module.webserver_cluster.aws_cloudwatch_metric_alarm.low_cpu_credit_balance: Creation complete after 1s (ID: GRSFBR-low-cpu-  credit-balance)

 Apply complete! Resources: 11 added, 0 changed, 0 destroyed.

 Outputs:

 elb_dns_name = GRSFBR-1116145917.us-east-1.elb.amazonaws.com
 Output from http://GRSFBR-1116145917.us-east-1.elb.amazonaws.com/: 
 Sleeping for 30 seconds and trying again
 Output from http://GRSFBR-1116145917.us-east-1.elb.amazonaws.com/: <h1>Hello, World</h1>
 <p>DB address: terraform-20190307133111016400000001.cbwxzimiiwhb.us-east-1.rds.amazonaws.com</p>
 <p>DB port: 3306</p>
 Success!
 
 Undeploying code in /home/nikolay/repos/book_examples/ch6/TF_Book_Ch_6/terraform-code/live/stage/services/webserver-cluster
 
 module.webserver_cluster.aws_cloudwatch_metric_alarm.high_cpu_utilization: Destruction complete after 1s
 module.webserver_cluster.aws_cloudwatch_metric_alarm.low_cpu_credit_balance: Destruction complete after 1s
 module.webserver_cluster.aws_security_group_rule.allow_server_http_inbound: Destruction complete after 1s
 module.webserver_cluster.aws_security_group_rule.allow_all_outbound: Destruction complete after 1s
 module.webserver_cluster.aws_security_group_rule.allow_http_inbound: Destruction complete after 2s
 aws_security_group_rule.allow_testing_inbound: Destruction complete after 4s
 module.webserver_cluster.aws_autoscaling_group.example: Destruction complete after 2m31s
 module.webserver_cluster.aws_launch_configuration.example: Destruction complete after 1s
 module.webserver_cluster.aws_elb.example: Destruction complete after 2s
 module.webserver_cluster.aws_security_group.instance: Destruction complete after 1s
 module.webserver_cluster.aws_security_group.elb: Destruction complete after 2m9s
 
 Destroy complete! Resources: 11 destroyed.
 
```
