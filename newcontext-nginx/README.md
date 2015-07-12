








newcontext-nginx
=====

Prerequisites

The latest version of virtual box should be installed to ensure that the Ansible server boxes 

specified in the playbook in this solution will run. For development and testing, Virtualbox 4.3.28 

for Windows x64 was used: (http://download.virtualbox.org/)



This playbook install the nginx package on a given host serving files from /usr/share/nginx/html directory.

A custom newcontext index file will be served from /usr/share/nginx/html.

To edit default subdirectory location change the location directive in the ./templates/nginx.conf.j2 file.

The ngnx service will run on port 8000 by default, to edit the default port make changes to the listen 
directive in the ./templates/nginx.conf.j2 file. 


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
 1 Edit the webserver directive in your /etc/ansible/hosts file or your local .ansible/hosts file (you can use a sample host file which is included herein)
 to include your target nginx server i.e. 10.10.10.108

 2 Edit the ansible_ssh_user id with your server's account ssh id.
 
 Example  /etc/ansible/hosts entry

 [webservers]
 
 10.10.10.108 ansible_ssh_user=root

 Note, this solution was tested on Ubuntu 13 and Ubuntu 14 LTS servers and will run with a sudo user id

 To run the ansible playbook:

``` bash
$ ansible-playbook newcontext-nginx.yml -k (provided you unstalled sshpass) to use the password on the command line

or


$ ansible-playbook newcontext-nginx.yml -K (if you are using ssh keys)

```

Prerequisites

The latest version of virtual box should be installed to ensure that the Ansible server boxes 

specified in the playbook in this solution will run. For development and testing, Virtualbox 4.3.28 

for Windows x64 was used: (http://download.virtualbox.org/)

Ansible is available for all major x86_64 OS's, including Linux: http://www.ansible.com

In addition, it is assumed that the user has a variant of git installed on their system in order to 

retrieve the author's solution from Github.

1. Describe the most difficult/painful hurdle you had to overcome in implementing your solution.

The most painful or difficult was deciding whether to use chef or ansible but I have decided on 

Ansible since it's simple, doesn't have any prerequisites apart from ssh and so does not assume 

that any agents are running on a target machine.

2. Describe which puppet related concept you think is the hardest for new users to grasp.

Although I did the project in Ansible, I believe that the hardest thing for the new Puppet users to 

grasp would be the catalog of classes.

3. Please comment on the concept embodied by the second requirement of the solution(ii)
ensure that subsequent applications of the solution do not cause failures or repeat redundant configuration tasks

The playbook should will only install nginx package if it is not installed already. The configuration files do get overwritten, but the playbook restarts services in between the configuration rewrites. 

4. Where did you go to find information to help you in the build process?

My own EverNotes and Google.

5. In a couple paragraphs explain what automation means to you and why it is important to an organization's infrastructure design strategy.

Automation is the process of enabling operating systems, software, and processes to independently perform mundane, often repeatable or time consuming tasks. For example when a company launches a new software product; normally this requires multiple new servers and service 'stacks' for development, testing & collaboration. In a world before automation a number of manual steps was required - installation, network and os provisioning, os and service configuration, as well as health & dependecy checks. In case of continous product delivery & integration, developers check in code daily and an individual build & deploy enviornment is created for each code commit.

These operations quickly become daunting and un-managable for most developers and devop teams. 

Automation frameworks drastically reduce these tasks to a  "push button" approach.
Humans are prone to error when attempting to repeat complicated multi-faceted technical tasks. 

That's why  automation is so important in a modern Development and IT design strategy. By automating many processes companies are able to reduce the risk, prevent accidents, and focus on the core business rather than wasting or duplicating efforts on tasks which can be safely automated. Successful modern enterprises can react and adopt quickly, thanks in part, to automation. In utilizing a consistent automation framework across one's business infrastructure, repeatable tasks become simplified and and the company saves both time and money.

It is easy to see the advantages and potential impact of automation pipelines and frameworks. Not only do the errors become drastically reduced, but new features can be added, changed and rolled out much quicker.

The effort and manpower needed to design, manage and deploy infrastructure is reduced.
Embracing automation results in a smoother running business which can quickly and 
successfully meet the demands of enterprise customers.
