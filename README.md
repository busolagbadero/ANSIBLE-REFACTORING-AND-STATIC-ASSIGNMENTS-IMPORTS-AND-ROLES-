# ANSIBLE-REFACTORING-AND-STATIC-ASSIGNMENTS-IMPORTS-AND-ROLES-
ANSIBLE REFACTORING AND STATIC ASSIGNMENTS (IMPORTS AND ROLES)


In this project, I'll improve ansible-config-mgt's repository by Refactoring Ansible code, creating assignments, and using imports.

I opened Jenkins-Ansible server and created a new directory called  ' ansible-config-artifact ' where i stored all artifacts after each build.

Used command 'sudo mkdir /home/ubuntu/ansible-config-artifact ' and changed permissions to this directory, so Jenkins could save files there  using command ' chmod -R 0777 /home/ubuntu/ansible-config-artifact ' 

![scl2](https://user-images.githubusercontent.com/94229949/193865541-9fa8e9bf-9c47-4ba8-89c8-1553b08c89aa.png)

Jenkins' 'Manage Jenkins' tab is where I installed the copy artifacts plugin. Jenkins wasn't restarted after installing Copy Artifact. Created a new Freestyle project named ' save_artifacts ' 

![scl3](https://user-images.githubusercontent.com/94229949/193869208-96cd0fe4-68e4-4817-9278-d32a3b23c5e8.png)

Configured the save_artifacts projects to be triggered at the  completion of the existing Ansible project.

![scl4](https://user-images.githubusercontent.com/94229949/193870727-49ebe77d-1896-468b-b235-1fe0dca48237.png)

![scl5](https://user-images.githubusercontent.com/94229949/193870765-c45dc158-af7f-4f68-9070-dc8915ee53c8.png)

![scl6](https://user-images.githubusercontent.com/94229949/193870792-fe0ecc01-dc42-4607-82c0-0ef4ee52a253.png)

Changed README.MD in ansible-config-mgt repository to test setup (right inside master branch).
Jenkins jobs were completed one after another and files were stored in /home/ubuntu/ansible-config-artifact and updated with every master commit.

![scl7](https://user-images.githubusercontent.com/94229949/193872421-a81d73f0-9032-472e-a3de-45b7b761dd1f.png)

I pulled down the latest code from master (main) and created a new branch, refactor.

In the playbooks folder, i created a file called  site.yml which will be the  entry point to the infrastructure setup. Site.yml will be the parent of all future playbooks.

Created static-assignments folder in repository root. The static-assignments folder holds all other children's playbooks. This is for easy organisation of my work.

Move common.yml file into the newly created static-assignments folder.

Inside site.yml file, import common.yml playbook.

![scl8](https://user-images.githubusercontent.com/94229949/193879345-c94c422e-ee61-488d-8891-39060e5a6260.png)

Since wireshark is already installed and I need to apply some tasks to dev servers, I created common-del.yml file under static-assignments. This playbook deletes wireshark. I ran  it against dev servers using command 'ansible-playbook -i inventory/dev.yml playbooks/site.yml'

![scl9](https://user-images.githubusercontent.com/94229949/193880804-02adfce7-b666-4de1-83fe-bb50e51fab85.png)

![scl10](https://user-images.githubusercontent.com/94229949/193880861-7315a81d-d4fc-47a5-adad-436f48962f46.png)

To confirm  wireshark has been  deleted on all the servers i ran  wireshark --version on each of the servers

![scl11](https://user-images.githubusercontent.com/94229949/193881382-52b9a511-08eb-411a-91ce-500bc65060c5.png)

![scl12](https://user-images.githubusercontent.com/94229949/193881415-f798a8a9-1897-4f0b-9a5d-9bcab30c0fae.png)

Configured UAT Webservers with a role ‘Webserver’

In order to create a role, I first made a directory that I called roles and then manually arranged the files and directories under the roles directory.

![scl150](https://user-images.githubusercontent.com/94229949/193884054-cbe4adb8-ac52-4007-85f4-950cb9f1f286.png)

Updated the  inventory ansible-config-mgt/inventory/uat.yml file with IP addresses of your 2 UAT Web servers

In /etc/ansible/ansible.cfg file ,i uncomment roles_path string and provided a full path to the roles directory roles_path    = /home/ubuntu/ansible-config-mgt/roles, so Ansible could know where to find configured roles.

I navigated to the tasks directory, and inside the main.yml file, I prepared the configuration tasks to carry out the activities listed below:
*Install and configure Apache (httpd service)
*Clone Tooling website from GitHub https://github.com/<your-name>/tooling.git.
*Ensure the tooling website code is deployed to /var/www/html on each of 2 UAT Web servers.
*Make sure httpd service is started







