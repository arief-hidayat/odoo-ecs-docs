
## Setup

In this section, we will setup VPC and other related resources manually.

We will show other approach using IaaC later.

### Create VPC and more

Search for `VPC` to go to VPC dashboard.
![search vpc](./static/001a-search-vpc.jpg)

Click `Create VPC` button
![create vpc](./static/001b-create-vpc.jpg)

Let's name it `odoo` and set IP CIDR to `10.1.0.0/16`
![set cidr](./static/001c-create-vpc.jpg)

VPC will span 2 AZs. each AZ will have 1 public subnets, 2 private subnets, and 1 NAT Gateway.
![set 2 az](./static/001d-create-vpc.jpg)

Can preview
![preview](./static/001e-create-vpc.jpg)

Then click `Create VPC` button
![confirm create vpc](./static/001f-create-vpc.jpg)

Wait until all resources are created
![wait for creation](./static/001g-vpc-created.jpg)

Can click left side menu. e.g. `VPC` menu.
![vpc list](./static/001h-vpc-created.jpg)

or `Subnets` etc.
![subnet list](./static/001i-subnets-created.jpg)

### Modify Turn Some Private to Isolated Subnets

In this case, we want to turn `private3` and `private4` subnets into isolated subnets (i.e. `isolated1` and `isolated2`).

So, `private1` and `private2` subnets can reach internet via NAT Gateway while `isolated1` and `isolated2` subnets can't.

Let's rename subnets accordingly
![rename subnets](./static/001j-subnets-renamed.jpg)

rename route tables as well
![rename route tables](./static/001k-route-tables-renamed.jpg)

select the isolated route table and click `edit routes`
![edit routes](./static/001l-edit-routes.jpg)

remove route to NAT GW
![remove route to NATGW](./static/001m-remove-route-to-natgw.jpg)

save change
![save route tables](./static/001n-save-change.jpg)

### Prepare IAM Roles for Cloud9 to Access Services


Go to `IAM` console. Select `Role` on the left menu. Then click `Create Role` button
![go to iam role](./static/003a-to-iam-role.jpg)

Select `AWS Service` and for `EC2` use case.
![go to iam role](./static/003b-create-for-ec2.jpg)

Search permission policy `AdministratorAccess` and tick the checkbox.
![admin](./static/003c-admin.jpg)


### Create Cloud9

Go to `Cloud9` console
![go to cloud9](./static/002a-to-cloud9.jpg)

Click `Create Environment`
![create environment](./static/002b-create-env.jpg)

Choose EC2 instance type. `t3.small` is good enough
![choose instance](./static/002c-t3-small.jpg)

Put it in our newly created VPC
![set VPC](./static/002d-use-our-vpc.jpg)

Use one of our private subnets
![set VPC](./static/002e-use-private-subnet.jpg)

Click `Create` button
![create env](./static/002f-create.jpg)

Once created, click `open`
![open env](./static/002g-created.jpg)

It will run the instance
![instance running](./static/002h-open-cloud9.jpg)

Back to the `cloud9` console, click name to see detail page
![cloud9 page](./static/002g-created.jpg)

Click `Manage EC2 Instance`
![manage ec2 instance](./static/002i-open-cloud9-detail.jpg)

New tab to `EC2` will be opened, click the checkbox
![select ec2](./static/002j-in-ec2-console.jpg)

Select from dropdown menu `Action` -> `Security` -> `Modify IAM Role`
![modify iam role](./static/002k-modify-iam-role.jpg)

Select IAM role we just created in previous step from dropdown menu.
![select iam role](./static/002l-update-iam-role.jpg)

Click `Update IAM Role`
![update iam role](./static/002m-update-iam-role.jpg)
