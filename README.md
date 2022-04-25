# EKS_C5_vs_C6i
Yaml configuration files to setup a EKS cluster to demonstrate performance gains of C5 vc C6i and also AVX2 vs AVX512.

Details about this workload and setup 
https://builders.intel.com/docs/networkbuilders/high-performance-computation-modernization-in-financial-services-industries-technology-guide-1617432497.pdf

<i>We are not exaclty using the same setup, we have taken a subset of the above instead of doing automated orchestration using Cloudify, we are applying the workload directly to EKS cluster and creating the cluster using eksctl instead of Terraform and Ansible etc. >/i>

Prerequistes : 
aws cli : https://docs.aws.amazon.com/polly/latest/dg/setup-aws-cli.html 
eksctl : https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html 

For our purpose we are using eksctl with config file setup
