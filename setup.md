<b>Step 1: </b><br/>
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
<b>Step 2 </b>: verify eksctl is installed "eksctl version",  you should see a version number <br />
<b>Step 3</b>: verify kubectl is installed "kubectl version" <br />
<b>Step 4</b>: now we are ready to create  our eks cluster as we have all the peices needed. Using the eksctl create command we will create the cluster using config file referred in this git repo  "EKS_demo.yml <br />
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
 
<b>Step 4</b>: we need to install Node Feature Discovery (NFD) (https://github.com/kubernetes-sigs/node-feature-discovery) <br />
use the command : <br /><br />
<b>kubectl apply -k https://github.com/kubernetes-sigs/node-feature-discovery/deployment/overlays/default?ref=v0.11.0 </b> <br />
<br />
<img src="/images/3_nfd_install.JPG" alt="kubectl NFD install" title="kubectl NFD install"> <br />
<br />

<b>Step 5</b> : now we will install the reporting namespaces which will setup prometheus, push gateway and grafan <br />

<b>kubectl apply -f reporting.yaml </b>  ( this will create pods and services needed)  <br />
<b>kubectl -n demo-reporting get all </b>  ( validate all are working fine)  <br />
<br />
<img src="/images/4_reporting_isntall.JPG" alt="kubectl reporting install" title="kubectl reporting install"> <br />
<br />


<b>Step 6 </b>: create the workload pods by applying pod specific yamls <br /><br />

<b>kubectl apply -f monte-carlo-c5-avx2.yaml </b> <br /><br />
<b>kubectl apply -f monte-carlo-c5-avx512.yaml </b><br /><br />
<b>kubectl apply -f monte-carlo-c6i-avx2.yaml </b><br /><br />
<b>kubectl apply -f monte-carlo-c6i-avx512.yaml </b><br />
<img src="/images/5_workloadpods.JPG" alt="kubectl pod workload" title="kubectl pod workload"> <br />
<br />

<br />

<b>Step 7</b>: At this point we have EKS cluster with 2 nodes, NFD , reporting setup done and workloads applied. Now we need to port forward the Grafana dashboard so we can see the visual of time elapased to do the mote carlo calculation on all our 4 pods. <br /><br />

<b>kubectl port-forward -n demo-reporting service/demo-reporting --address 0.0.0.0 3000:3000 9090:9090 9091:9091 </b> <br />

Now we can go to localhost port 3000 and default username is "admin" and password is in the reporting yaml default of "password" <br />
http://localhost:3000/ 
<br />
<img src="/images/6_grafana_login.JPG" alt="grafana login" title="grafana login"> <br />
<br />
<img src="/images/7_grafana_dashboard.JPG" alt="grafana select dashboard" title="grafana select dashboard"> <br />
<br />
<img src="/images/8_final_dashboard.JPG" alt="grafana final dashboard" title="grafana final dashboard"> <br />

<br />

<h16>Demo Up and Running!!!</h16>

<br />

<b> NOTE please delete your workloads and node if you are not using it for demo or learning as its going to cost $$$ <b>
    
 Step 8 : <br />
DELETE Options  1 : Quick and Dirty delete the EKS CLUSTER using EKSCTL <br />
    
    eksctl delete cluster --name <prod> --region <regioncode> <br />
    
  DELETE Options  2 :  <br />
  Delete workloads :    <br />
<b>kubectl delete -f monte-carlo-c5-avx2.yaml</b> <br />
<b>kubectl delete -f monte-carlo-c5-avx512.yaml </b><br />
<b>kubectl delete -f monte-carlo-c6i-avx2.yaml</b> <br />
<b>kubectl delete -f monte-carlo-c6i-avx512.yaml</b> <br />
  <br />
    
    Delete Reporting setup : <br />
 <b>   kubectl delete -f reporting.yaml</b>
    <br />
    
    Delete NFD : <br />
    
   <b>  kubectl delete -k https://github.com/kubernetes-sigs/node-feature-discovery/deployment/overlays/default?ref=v0.11.0  </b>
    <br />
    
    Delete EKS CLuster: <br />
    eksctl delete cluster --name <clustername> --region <regioncode> <br />
