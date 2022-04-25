# EKS_C5_vs_C6i

Our source for reference is the following document and material created by Intels Team.. special thanks to Petar Torre and team. <br />
https://builders.intel.com/docs/networkbuilders/high-performance-computation-modernization-in-financial-services-industries-technology-guide-1617432497.pdf <br />

Financial Services Workload Samples: <br /> 
https://github.com/intel/Financial-Services-Workload-Samples

<i>We are not exaclty using the same setup, we have taken a subset of the above instead of doing automated orchestration using Cloudify, we are applying the workload directly to EKS cluster and creating the cluster using eksctl instead of Terraform and Ansible etc. <br />
Intent is so we can setup this as a lab quicky for a presentation to show perfroamnce gains using instances and features like avx2 vs avx512 <br />

This repo is not intending to Replace the core documentation and material, its a mere intent to have it setup quikly for local setup and demo</i>
<br />

<b>NOTE: We are setting up a demo enviornment for our usecase, it is not a example of setting up a Production EKS cluster </b>

Prerequistes : <br />
aws cli : https://docs.aws.amazon.com/polly/latest/dg/setup-aws-cli.html  <br />
eksctl : https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html <br />
kubectl : https://kubernetes.io/docs/tasks/tools/ <br />


  <br />
  <br />
  
 <b>High level reference architecture and setup </b><br />

<img src="/images/subset_C5_C6i_avx2_avx215_setup.jpg" alt="High level reference" title="High level reference"> <br />

<b>Pod setup and metrics flow </b><br />
<img src="/images/pod_setup_metrics_collection.jpg" alt="Pod setup and metrics flow" title="Pod setup and metrics flow"> <br />

<b>Demo summary dashboard </b> <br />
<img src="/images/demo_summry_dashboard.jpg" alt="Pod setup and metrics flow" title="Pod setup and metrics flow"> <br />
