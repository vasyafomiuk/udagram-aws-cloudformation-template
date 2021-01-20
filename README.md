# This is a cloudformatino AWS tempalte

**To be able to use this template, first you need to create params.json file:**

```json
[
	{
		"ParameterKey": "KeyName",
		"ParameterValue": "my-key"
	},
	{
		"ParameterKey": "InstanceTypeParameters",
		"ParameterValue": "t2.micro"
	},
	{
		"ParameterKey": "EnvironmentName",
		"ParameterValue": "env"
	},
	{
		"ParameterKey": "VpcCIDR",
		"ParameterValue": "10.0.0.0/16"
	},
	{
		"ParameterKey": "PublicSubnet1CIDR",
		"ParameterValue": "10.0.0.0/24"
	},
	{
		"ParameterKey": "PublicSubnet2CIDR",
		"ParameterValue": "10.0.1.0/24"
	},
	{
		"ParameterKey": "PrivateSubnet1CIDR",
		"ParameterValue": "10.0.2.0/24"
	},
	{
		"ParameterKey": "PrivateSubnet2CIDR",
		"ParameterValue": "10.0.3.0/24"
	}
]
```

**Then, update user data for your servers. Specify some application server to spin up or use docker with some image.**

      UserData:
        Fn::Base64: !Sub |
          #!/bin/bash
          sudo apt-get update -y
          sudo apt-get install unzip awscli -y
          sudo apt-get install apache2 -y
          sudo systemctl start apache2.service
          cd /var/www/html
          sudo aws s3 cp s3://vasulok-bucket/udacity.zip .
          sudo unzip -o udacity.zip

**To create a stack, run setup.sh file. This file is also used for updating stack.**

`./setup.sh`

**Example of working configuration, you can view by clicking following link:**

[Click to view website example](http://udagr-webap-1mhjh7d5699mk-1589012040.us-west-2.elb.amazonaws.com/)