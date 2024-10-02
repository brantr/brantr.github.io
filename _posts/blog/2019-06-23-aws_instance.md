---
layout: post
categories: blog
title: AWS Instances
use_math: true
---

* Table of Contents
{:toc}


# AWS Instances

Some instructions for creating, using, and terminating AWS instances.


## Sign In

Navigate to [AWS](https://aws.amazon.com/). Click on AWS Management Console from the drop down. Log in, use Google Authenticator for MFA.

## Start EC2 Instance

Click EC2.  Click the blue Launch Instance button. Select Ubuntu Server 18.04 LTS (64-bit x86). Click t2.micro for tests (Free tier eligible).  

Click gray Configure Installation Details button.

Click shutdown behavior->terminate.  Click Next: Add Storage.

Can add Elastic Block Store. AWS Free Tier includes 30GB storage, 2million I/Os, and 1GB of snapshot storage. 
Default is 8 GiB. If this works, click Next: Add Tags button.

Add a Tag for this instance.

If all good, click blue Review and Launch button. Review, then click blue Launch button.

Click "Create a new key pair" from drop down. Create a name. Click Download Key Pair. Save the .pem somewhere. Click Launch Instances.

## Connect to the EC2 Instance

Click View Instances.  Find your running instance. Scroll through Description to check that the key pair is what you think it should be. Change the permissions of the .pem to 400. The username is "ubuntu". The instance name is listed under Description tab, has a copy icon. Connect via, e.g., 
{% highlight bash%}
#local machine  
ssh -i key_filename.pem ubuntu@ec2-3-14-14-27.us-east-2.compute.amazonaws.com 
{% endhighlight %}


## Now What?

First, you can verify the disk size:
{% highlight bash%}
ubuntu@ip-172-31-39-122:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            481M     0  481M   0% /dev
tmpfs            99M  736K   98M   1% /run
/dev/xvda1      7.7G  1.1G  6.7G  14% /
tmpfs           492M     0  492M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           492M     0  492M   0% /sys/fs/cgroup
/dev/loop0       91M   91M     0 100% /snap/core/6350
/dev/loop1       18M   18M     0 100% /snap/amazon-ssm-agent/930
tmpfs            99M     0   99M   0% /run/user/1000
ubuntu@ip-172-31-39-122:~$
{% endhighlight %}

Note that it's 7.7GB == 8 GiB.  Can install everything via apt. For instance:

### Update apt

{% highlight bash%}
sudo apt update
{% endhighlight %}


### Install pip3 (will get gcc, most python3)

{% highlight bash%}
sudo apt-get install python3-pip
{% endhighlight %}

Some services w/ libssl will need to be restarted, but should not disconnect.

### Install numpy and scipy.
{% highlight bash%}
ubuntu@ip-172-31-39-122:~$ sudo -H pip3 install numpy scipy
Collecting numpy
  Downloading https://files.pythonhosted.org/packages/87/2d/e4656149cbadd3a8a0369fcd1a9c7d61cc7b87b3903b85389c70c989a696/numpy-1.16.4-cp36-cp36m-manylinux1_x86_64.whl (17.3MB)
    100% |████████████████████████████████| 17.3MB 76kB/s
Collecting scipy
  Downloading https://files.pythonhosted.org/packages/72/4c/5f81e7264b0a7a8bd570810f48cd346ba36faedbd2ba255c873ad556de76/scipy-1.3.0-cp36-cp36m-manylinux1_x86_64.whl (25.2MB)
    100% |████████████████████████████████| 25.2MB 49kB/s
Installing collected packages: numpy, scipy
Successfully installed numpy-1.16.4 scipy-1.3.0
{% endhighlight %}


## Terminate the Instance

Click Actions->Instance State->Terminate.  It will destroy the EBS, so move any data off first.

