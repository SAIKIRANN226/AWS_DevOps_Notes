### How to create multiple environments with terraform in 3 ways
- Terraform.tfvars
- Workspaces
- Different repos for different environments
### Terraform.Tfvars method
For example we want web-dev/mongodb-dev/catalogue-dev/redis-dev/user-dev/cart-dev etc.
                    web-qa/mongodb-qa/catalogue-qa/redis-qa/user-qa/cart-qa etc.
                    web-uat/mongodb-uat/catalogue-uat/redis-uat/user-uat/cart-uat etc.
                    web-prod/mongodb-prod/catalogue-prod/redis-prod/user-prod/cart-prod etc
Domain names are ---> web-dev.megacitysai.fun, mongodb-qa.megacitysai.fun, etc.

Same code but with different configuration, that means we need to control using variables for different 
env's by using tfvars. Different buckets to maintain states by creating different folders "dev,prod". 
What do you think ? Using different buckets for dev and prod, or one bucket ? different is the best, 
we can also use one bucket for both dev and prod, but we make sure different evn's should not get disturbed. How do we maintain different buckets ? By creating two buckets for dev and prod in "AWSconsole" and also create dynamodb tables for dev and prod.
