Step 1: <br /> <br />

Verify awscli is installed, connected and working, run the command to verify "aws iam get-user"  output should look something like <br />
{
    "User": {<br />
        "Path": "/",<br />
        "UserName": "username",<br />
        "UserId": "AXXXXYYYYYZZZZZZZZZ",<br />
        "Arn": "arn:aws:iam::accountnumber:user/user-cli",<br />
        "CreateDate": "2022-01-21T18:44:28+00:00",<br />
        "Tags": [<br />
            {<br />
                "Key": "usertype",<br />
                "Value": "cli"
            }
                  ]
             }
        }
<br />

Step 2: verify eksctl is installed "eksctl version" <br /> you should see a version number
<br />

Step 3: verify kubectl is installed "kubectl version" <br />

Step 4: now we are ready to create  our eks cluster as we have all the peices needed. Using the eksctl create command we will create the cluster using config file referred in this git repo  "EKS_demo.yml <br />
eksctl create cluster -f EKS_demo.yml <br />

output similar to this in command line
<img src="/images/1_eksctl_create.JPG" alt="eksctl create cluster" title="eksctl create cluster"> <br />
<br />

Be patient this is going to take some time .. close to <b>15ishh min</b> <br />
once completed it should show screen similar to following <br />
<img src="/images/2-eksctl_create_done.JPG" alt="eksctl create cluster done " title="eksctl create cluster done"> <br />

Run command <br />
<b>kubectl get nodes </b><br />

 you should see 2 nodes :) 

Step 4: we need to install Node Feature Discovery (NFD) (https://github.com/kubernetes-sigs/node-feature-discovery) <br />
use the command : <br /><br />
<b>kubectl apply -k https://github.com/kubernetes-sigs/node-feature-discovery/deployment/overlays/default?ref=v0.11.0 </b> <br />
<br />
<img src="/images/3_nfd_install.JPG" alt="kubectl NFD install" title="kubectl NFD install"> <br />
<br />

Step 5 : now we will install the reporting namespaces which will setup prometheus, push gateway and grafan <br />

<b>kubectl apply -f reporting.yaml </b>  ( this will create pods and services needed)  <br />
<b>kubectl -n demo-reporting get all </b>  ( validate all are working fine)  <br />
<br />
<img src="/images/4_reporting_isntall.JPG" alt="kubectl reporting install" title="kubectl reporting install"> <br />
<br />


Step 6 : create the workload pods by applying pod specific yamls <br /><br />

<b>kubectl apply -f monte-carlo-c5-avx2.yaml </b> <br /><br />
<b>kubectl apply -f monte-carlo-c5-avx512.yaml </b><br /><br />
<b>kubectl apply -f monte-carlo-c6i-avx2.yaml </b><br /><br />
<b>kubectl apply -f monte-carlo-c6i-avx512.yaml </b><br />
<img src="/images/5_workloadpods.JPG" alt="kubectl pod workload" title="kubectl pod workload"> <br />
<br />





