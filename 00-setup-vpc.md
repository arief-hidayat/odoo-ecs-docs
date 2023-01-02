
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
