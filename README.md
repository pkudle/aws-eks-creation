# Deploy your first EKS cluster on AWS using below steps

Steps -
1) Navigate to AWS EKS service
2) Select create cluster option.. It gives two modes - 1) Auto 2) Custom
3) Select Custom config mode
4) In cluster config mode, select Kubernetes version & cluster role
5) Steps to create cluster role -> 1) Go to IAM service 2) Select create role and give permissions. ( AmazonEKSClusterPolicy )
6) Post cluster role selection, select specify networking options.. ( in which VPN, subnets you need your EKS cluster )
7) Configure observability for metrics and API logs of EKS if needed or you can skip it
8) Select add-ons ( plugins ) which would be needed by EKS cluster. I kept already selected one's / default one's
9) Review the options selected and click on create

Note - AWS doesnt allow no of master nodes selection while deploying the cluster using AWS EKS. It automatically takes care of it, as per the load / incoming traffic as per observality metrics. However you can specify how many worker nodes are needed using auto scaling configuration while creation of node groups..

Steps for NodeGroup creation
1) Post EKS cluster creation, go to Compute section
2) In side compute section, go to Nodegroups view and click on add node group
3) Post this, give node group name and node group IAM role.
4) Steps to create node group iam role -> 1) Go to IAM service 2) Select create role and give permissions. ( AmazonEC2ContainerRegistryReadOnly, AmazonEKS_CNI_Policy, AmazonEKSClusterPolicy, AmazonEKSWorkerNodePolicy )
5) Post node group role creation, select node group compute configuration.
6) In this step, you would need to specify ami details, instance type, node group scaling config ( desired, min, max ) , node group repair etc. configuration
7) Post this, specify the networking details like - vpn, subnet etc.
8) Review the option and click on create
9) Post this, under cluster.. you can view node group creation status
10) Additionally, you can also switch to ec2 service, to check the instances which are going to get created as part of this nodegroup..

How to Validate -

Using cloudshell on AWS -
1) use command - aws eks update-config --region <region-name> --cluster <cluster-name>
2) this adds/updates cluster details in .kube/config
3) use kubectl commands to verify the cluster info and node status..

Using Local Terminal/Bastian Node or remote machine to access EKS cluster
1) Install aws cli and kubectl
2) use command - aws configure.. to configure the IAM user who has permission to access eks cluster. Enter access id and secret along with region name
3) use command - aws eks update-config --region <region-name> --cluster <cluster-name>
4) use command like - kubectl get nodes ( To check node status) , kubectl get pods ( to view running pods etc)
