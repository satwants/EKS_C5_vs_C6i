Step 1: <br /> <br />

Verify awscli is installed, connected and working, run the command to verify "aws iam get-user"  output should look something like <br />
{<br />
    "User": {<br />
        "Path": "/",<br />
        "UserName": "username",<br />
        "UserId": "AXXXXYYYYYZZZZZZZZZ",<br />
        "Arn": "arn:aws:iam::accountnumber:user/user-cli",<br />
        "CreateDate": "2022-01-21T18:44:28+00:00",<br />
        "Tags": [<br />
            {<br />
                "Key": "usertype",<br />
                "Value": "cli"<br />
            }<br />
                  ]<br />
             }<br />
        }<br />

<br />

Step 2: verify eksctl is installed "eksctl version" <br /> you should see a version number
<br />

Step 3: verify kubectl is installed "kubectl version" <br />

Step 4: now we are ready to create  our eks cluster as we have all the peices needed. Using the eksctl create command we will create the cluster using config file referred in this git repo  "EKS_demo.yml <br />
"eksctl create cluster -f EKS_demo.yml" <br />

output similar to this in command line
<img src="/images/1_eksctl_create.JPG" alt="eksctl create cluster" title="eksctl create cluster"> <br />






