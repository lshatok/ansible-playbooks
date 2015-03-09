nginx
=====

## nginx

# This playbook install the nginx package in the subdirectory of /nwea-techops/tech_quiz on a given host.
# To edit default subdirectory location change the location directive in the ./templates/nginx.conf.j2 file.

# The ngnx service will run on port 8888 by default, to edit the default port make changes to the listen 
# directive in the ./templates/nginx.conf.j2 file. 


### Vars

* **delete_default_vhost**: Delete or not default vhost
    * Type: Boolean
    * Default: false
* **user**:
    * Type: String
    * Default: www-data
* **worker_processes**:
    * Type: Integer
    * Default: $ansible_processor_count
* **pid**:
    * Type: String
    * Default: /var/run/nginx.pid
* **worker_connections**:
    * Type: Integer
    * Default: 768

### Usage ###
# 1 Edit the webserver directive in your /etc/ansible/hosts file or your local .ansible/hosts file
# to include your target nginx server i.e. github.com
# 2 Edit the ansible_ssh_user id with your github account ssh id.


## Example  /etc/ansible/hosts entry
# 
# [webservers]
# github.com ansible_ssh_user=jed

# Note, this solution was tested on Ubuntu 13 and Ubuntu 14 LTS servers and will run with a sudo user id

# To run the ansible playbook


``` bash
$ ansible-playbook nginx.yml -K 
```

#### you will be asked for your user's password 



## vhost-redirect

This playbook add a simple redirect vhost for nginx.

### Vars

* **name**: The vhost name
    * Type: String
    * Default: redirect_$server_name
* **listen**:
    * Type: String
    * Default: *:8888
* **server_name**: The server domain name
    * Type: String
    * Default:  defined in ansible webservers hosts directive
* **redirect_url**: The redirect URL
    * Type: String
    * Default: http://www.$server_name
