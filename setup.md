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

