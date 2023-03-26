Pre requiste:

Install SSM plugin :
Please follow the documentation for the same.
https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html#install-plugin-windows

![image](https://user-images.githubusercontent.com/26665659/227767396-96e578f3-cf8a-472f-836b-8eae04dd48de.png)




Install AWS CLI plugin:
Please follow the documentation below:





As mentioned before, the SSM agent is running on most EC2 instances already.
That’s because the agent is bundled into Amazon Linux, Amazon Linux 2, SUSE Linux
Enterprise Server (12 and 15), and Ubuntu Server (16.04, 18.04, and 20.04) by default.



However, the SSM agent requires an IAM role attached to the EC2 instance granting
access to the SSM API. That’s not a default, so you probably need to create a new IAM
role or add a policy to existing roles.


Predefined policy:
AmazonSSMManagedInstanceCore



create your own managed or in-line policy with the following contents:


{
"Version": "2012-10-17",
"Statement": [
{
"Effect": "Allow",
"Action": [
"ssmmessages:*",
"ec2messages:*",
"ssm:UpdateInstanceInformation"
],
"Resource": "*"
}
]
}


