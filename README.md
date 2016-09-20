# What is this?

It's an ansible playbook, designed primarily for usage with BAWS Builder at https://baws.io to build high performance, PHP driven, Drupal or WordPress optimized serverss, on the Linux AMI. 

Since BAWS Builder is just a GUI, you may use this without BAWS builder if you're familiar with AWS. However, BAWS Builder was developed for a reason; it simplifies a lot of tedious tasks.

This is in alpha stages, and still contantly evolving. Some bugs expected. Feedback welcome.

#Requirements.
Certain functions may require IAM Roles attached to your instance or proper security group configuration in order to access functions such as creating storage or attaching EFS.

You will need to set Public IP to enabled (Load balancers or proxies are outside the scope of these examples).

While local VM and Debian family support is on the road map, some functionality, such as CodeDeploy, is inherently exclusive to AWS.

#Usage

If you'd like to use this playbook directly, without BAWS builder,  Copy and paste examples below into the User Data field when launching an AMI. This is currently under Step 3 under the "Advanced" section.

##Quick start: Some examples to get started quickly
Replace all `example` instances with your own values.

```bash
#!/bin/bash

yum install git -y
pip install ansible

su ec2-user -c '/usr/local/bin/ansible-pull -U "https://github.com/wwwpro/baws_ansible.git" \
--tags="dev,webtools,grav" \
--extra-vars="{"user_email": example@example.com, "user_name": "example"}"'

```

##What's happening above

Tags largely define how the server gets built. Typically either `dev`  or `live` tags are used on every web server. Both tags will build an Nginx and PHP-FPM based web server. Dev includes extra pools, installs xdebug and makes extra tweaks for easier developing. While `live` maximizes caching and efficency and minimizes extra packages.

`webtools` installs typical web utilities such a PhpMyAdmin and OpCacheGUI.

`grav` installs Grav, flat-fils CMS as the default website.

Note that MySQL is not installed by default. Add the `mysql` tag to install it. 

More samples coming soon. Stay tuned.


