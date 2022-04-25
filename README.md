# EKS_C5_vs_C6i

Monte Carlo simulation is commonly used to evaluate the risk and uncertainty that would affect the outcome of different decision
options. Monte Carlo methods are used in corporate finance and mathematical finance to value and analyze (complex) instruments,
portfolios, and investments by simulating the various sources of uncertainty affecting their value, and then determining the
distribution of their value over the range of resultant outcomes. <br/>
Monte Carlo algorithms are used to calculate the value of an option with multiple sources of uncertainties and random features,
such as changing interest rates, stock prices or exchange rates, etc. to evaluate complex instruments, portfolios, and investments.
Monte Carlo European options is a numerical method that uses statistical sampling techniques to approximate solutions to
quantitative problems. This is a compute-bound, double precision workload and benefits from Intel® Turbo Boost Technology and
Intel® Hyper-Threading Technology.<br/>
Such simulations are based on vector type random number generators. Intel Advanced Vector Extensions 512 (Intel AVX-512) is a
set of instructions that can accelerate performance for workloads and usages such as scientific simulations, financial analytics,
artificial intelligence (AI)/deep learning, 3D modeling and analysis, image and audio/video processing, cryptography and data
compression.<br/>
Previous Intel® AVX2 contained most vector instructions of 256 bits. Intel AVX-512 doubles that width to 512 bits and can boost
performance for such demanding workloads.<br/>
There can be many types of Monte Carlo simulations with different requirements such as desired time to complete, or sensitivity
from other workloads etc. As a baseline for this guide, we assumed that simulation run needs to complete under certain time that
can vary slightly. It is also possible to configure the systems for more sensitive workloads requiring more predictability or for more
resilient (less sensitive) workloads that can run in shared cloud environments with impairments coming from the workload of other
tenants.<br/>
The achieved results show that the elapsed time to complete simulation runs with Intel AVX-512 is about half of the time taken with
Intel AVX2. This result correlates with doubling the width of vector instructions used.<br/> <br/>

Our source for reference is the following document and material created by Intels Team.. special thanks to <b>Petar Torre</b> and team. <br />
https://builders.intel.com/docs/networkbuilders/high-performance-computation-modernization-in-financial-services-industries-technology-guide-1617432497.pdf <br />

Financial Services Workload Samples: <br /> 
https://github.com/intel/Financial-Services-Workload-Samples

<i>We are not exaclty using the same setup, we have taken a subset of the above instead of doing automated orchestration using Cloudify, we are applying the workload directly to EKS cluster and creating the cluster using eksctl instead of Terraform and Ansible etc. <br />
Intent is so we can setup this as a lab quicky for a presentation to show performance gains using instances<b> C5 vs C6i and avx2 vs avx512 </b> <br />

This repo is not intending to Replace the core documentation and material, its a mere intent to have it setup quikly for local setup and demo</i>
<br />

<b>NOTE: We are setting up a demo environment for our usecase, it is not a example of setting up a Production EKS cluster </b>

Prerequistes tool installs : <br />
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
