## Context

We have prepared [git repo](https://github.com/arief-hidayat/odoo-ecs) which contains [CDK](https://aws.amazon.com/cdk/) project.

## Prepare Repo

Clone repo
```
git clone https://github.com/arief-hidayat/odoo-ecs.git
cd odoo-ecs/
npm install
cdk bootstrap

```
Open file `odoo-ecs/lib/odoo-ecs-stack.ts `, edit email and VPC name. firstTime to `true`
```
    const emailAddress = 'mr.arief.hidayat@gmail.com';
    ...
    const firstTime = false;
    ...
    const vpc = ec2.Vpc.fromLookup(this, 'dev-vpc', {vpcName: 'AriefhInfraStack/dev-vpc'});
```

generate cloudformation template 
```
cdk synth
```

### Deploy
deploy
```
cdk deploy
```

