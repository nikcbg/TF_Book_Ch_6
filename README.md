# TF_Book_Ch_6


### The purpose of the repository is to show example code on how to use terraform as a team.

#### Check the links below for terraform example code and explanation on what the code does in each folder:
-----------------------------------------------------------------------------------------------------------

#### Configuration code that imports IAM user that already exists in AWS 
                        
1.[terraform-code/modules/services/webserver-cluster](https://github.com/nikcbg/TF_Book_Ch_6/tree/master/terraform-code/modules/services/webserver-cluster)- Terraform configuration code that is used as module to create webservers cluster and load balancer in AWS.

--------------------------------------------------------------------------------------------------------

#### Configuration code that creates MySQL database in AWS (production environment)
 
6.[terraform-code/live/prod/data-stores/mysql](https://github.com/nikcbg/TF_Book_Ch_6/tree/master/terraform-code/live/prod/data-stores/mysql) - Terraform configuration code in prod folder that creates MySQL database which talks to webservers cluster.

------------------------------------------------------------------------------------------------------------------

#### Configuration code that creates webservers cluster and load balancer in AWS using a module (production environment).
                    
7.[terraform-code/live/prod/services/webserver-cluster/](https://github.com/nikcbg/TF_Book_Ch_6/tree/master/terraform-code/live/prod/services/webserver-cluster) - Terraform configuration code in prod folder that uses the code in module folder to create webservers cluster and load balancer in AWS.

------------------------------------------------------------------------------------------------------------------

#### Configuration code that creates MySQL database in AWS (staging environment)
                    
8.[terraform-code/live/stage/data-stores/mysql](https://github.com/nikcbg/TF_Book_Ch_6/tree/master/terraform-code/live/stage/data-stores/mysql) - Terraform configuration code in stage folder that creates MySQL database which talks to webservers cluster.

------------------------------------------------------------------------------------------------------------------

#### Configuration code that creates webservers cluster and load balancer in AWS using a module (staging environment).
                    
9.[terraform-code/live/stage/services/webserver-cluster](https://github.com/nikcbg/TF_Book_Ch_6/tree/master/terraform-code/live/stage/services/webserver-cluster) - Terraform configuration code in stage folder that uses the code in module folder to create webservers cluster and load balancer in AWS.

------------------------------------------------------------------------------------------------------------------

#### Ruby code 
                    
10.[ruby-code](https://github.com/nikcbg/TF_Book_Ch_6/tree/master/ruby-code) - 

------------------------------------------------------------------------------------------------------------------

