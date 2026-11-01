# HCP Terraform Intra Region VPC Peering with VCS Driven Using Main Branch and folder wildcard patterns

Date: October 25, 2026 7:28 PM
Git Repo: https://github.com/Htaung/hcp-terraform-vpc-peering-remote
Hands on: Done
References: https://link.excalidraw.com/readonly/yfziGTVaJOPPLQ3VIHtM
URL: https://www.youtube.com/watch?v=vPPqY0WSbnU

#### Create VCS provider under terraform cloud

- Organization > Setting > Providers > Add VCS Provider
- 

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image.png)

#### Create new OAuth application in git hub

[https://developer.hashicorp.com/terraform/enterprise/vcs/github](https://developer.hashicorp.com/terraform/enterprise/vcs/github)

- **create a new OAuth application**
- Take the Application Name, HomePage and CallbackURL from terraform cloud and register in github.
- Web hooks was automatically created by github

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%201.png)

- Genereate client secret and copy client id and secret to terraform cloud vcs provider

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%202.png)

- Add client id and secret in terraform cloud VCS Provider

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%203.png)

- Give Authorization

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%204.png)

- Skip and finish

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%205.png)

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%206.png)

- Create new workspace and choose empty repo from git hub https://github.com/Htaung/hcp-terraform-vpc-peering-remote
- Add terraform source code to git
- Add github folder name, path in terraform cloud

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%207.png)

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%208.png)

- Setup dynamic credential

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%209.png)

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2010.png)

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2011.png)

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2012.png)

- First time have to invoke manually trigger once

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2013.png)

- After start new run

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2014.png)

- After start new run manually ⇒ git push into fe-network and check new run was start automatically

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2015.png)

- After git push not started new task in terrafrom
- Change the patterns

```jsx
Syntax
Switching between patterns and prefixes will cause the previously saved values 
to be replaced. To reverse this action, they will have to be re-entered. 

fe-network/**/* 
```

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2016.png)

- Create new workspace fe-security-ws
- workspace name must match in terraform code’s version
- patterns ⇒ fe-security/**/*

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2017.png)

- Create dynamic credential
- audience test.oidc

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2018.png)

```jsx
TFC_AWS_APPLY_ROLE_ARN
TFC_AWS_PLAN_ROLE_ARN
TFC_AWS_PROVIDER_AUTH
TFC_AWS_WORKLOAD_IDENTITY_AUDIENCE
```

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2019.png)

- Trigger manually first

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2020.png)

- Git commit and push “Add space”, terraform will run automatically after git push

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2021.png)

- Do the same steps for fe-compute-ws, be-network-ws, be-security-ws, be-compute-ws

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2022.png)

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2023.png)

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2024.png)

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2025.png)

- Getting key file from state file / have to research best practise

```jsx
get key file from state file that have escapce chars 
fe_instances_private_key

copy 

sed 's/\\n/\n/g' fe_raw.txt > fe.pem
chmod 400 fe.pem

```

![image.png](HCP%20Terraform%20Intra%20Region%20VPC%20Peering%20with%20VCS%20Dr/image%2026.png)