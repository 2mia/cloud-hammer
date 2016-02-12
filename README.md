#### What?

- quick way to hammer your cloud formation to match your local templates.
- a better name would have been cloud-formation-sync or cloud-sync; the 1st is too long, the 2nd is misleading - we don't upload files

#### Install it

    sudo bash -c "curl https://raw.githubusercontent.com/2mia/cloud-hammer/master/cloud-hammer > /usr/local/bin/cloud-hammer && chmod 755 /usr/local/bin/cloud-hammer"

Install `jq`

    sudo bash -c "curl http://stedolan.github.io/jq/download/linux64/jq > /usr/local/bin/jq && chmod 755 /usr/local/bin/jq"

#### Quick how to

execute `./cloud-hammer your-stack-name  demo.json`


Execution samples

#### update security groups

    [user@osx ~/dev/cloud-hammer] (master)# ./cloud-hammer your-stack-name  demo.json
    hammer understood this: your-stack-name demo.json demo.properties
        check param: VPC => vpc-1234
        check param: AZ1 => us-east-1a
        check param: AZ2 => us-east-1b
        check param: SubnetPub1 => subnet-1234
        check param: SubnetPub2 => subnet-2345
        check param: KeypairName => keypairs
    [*] calculating update - diff
    249,278d248
    <             "FromPort": "22",
    <             "IpProtocol": "tcp",
    <             "ToPort": "22"
    <           },
    <           {
    <             "CidrIp": "169.152.22.5/32",
    <             "FromPort": "22",
    <             "IpProtocol": "tcp",
    <             "ToPort": "22"
    <           },

    Are you sure to apply the changes? y
    [*] updating stack your-stack-name ....
    {
        "StackId": "arn:aws:cloudformation:us-east-1:xxxxx:stack/your-stack-name/aa22-50d5017c76e0"
    }



#### update AMI ids

    user@osx ~/dev/cloud-hammer] (master)# ./cloud-hammer your-stack-name  demo.json
    hammer understood this: your-stack-name demo.json demo.properties
        check param: VPC => vpc-1234
        check param: AZ1 => us-east-1a
        check param: AZ2 => us-east-1b
        check param: SubnetPub1 => subnet-1234
        check param: SubnetPub2 => subnet-2345
        check param: KeypairName => keypairs
    [*] calculating update - diff
    22c22
    <         "PV64": "ami-f8f44490"
    ---
    >         "PV64": "ami-ed8e9284"

    Are you sure to apply the changes? y
    [*] updating stack your-stack-name ....
    {
        "StackId": "arn:aws:cloudformation:us-east-1:xxxxxx:stack/your-stack-name/aa22-50d5017c76e0"
    }

