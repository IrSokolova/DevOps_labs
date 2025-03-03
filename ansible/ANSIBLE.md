# Lab 5
## Playbook

```
 ansible-playbook ansible/playbooks/dev/main.yaml --diff
```

The output:

```

PLAY [Prepare docker] ******************************************************************************************************************************************************************************************************************

TASK [docker : include_tasks] **********************************************************************************************************************************************************************************************************
included: /home/irina/PycharmProjects/DevOps_labs/ansible/roles/docker/tasks/install_docker.yml for localhost

TASK [docker : Install Docker packages.] ***********************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [docker : Ensure /etc/docker/ directory exists.] **********************************************************************************************************************************************************************************
skipping: [localhost]

TASK [docker : Configure Docker daemon options.] ***************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [docker : Ensure Docker is started and enabled at boot.] **************************************************************************************************************************************************************************
ok: [localhost]

TASK [docker : include_tasks] **********************************************************************************************************************************************************************************************************
included: /home/irina/PycharmProjects/DevOps_labs/ansible/roles/docker/tasks/install_compose.yml for localhost

TASK [docker : Check current docker-compose version.] **********************************************************************************************************************************************************************************
ok: [localhost]

TASK [docker : set_fact] ***************************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [docker : Delete existing docker-compose version if it's different.] **************************************************************************************************************************************************************
--- before
+++ after
@@ -1,4 +1,4 @@
 {
     "path": "/usr/local/bin/docker-compose",
-    "state": "file"
+    "state": "absent"
 }

changed: [localhost]

TASK [docker : Install docker-compose plugin.] *****************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [docker : Install docker-compose-plugin (with downgrade option).] *****************************************************************************************************************************************************************
skipping: [localhost]

TASK [docker : Ensure handlers are notified now to avoid firewall conflicts.] **********************************************************************************************************************************************************

TASK [docker : Get docker group info using getent.] ************************************************************************************************************************************************************************************
skipping: [localhost]

PLAY RECAP *****************************************************************************************************************************************************************************************************************************
localhost                  : ok=6    changed=1    unreachable=0    failed=0    skipped=6    rescued=0    ignored=0 
```

## Inventory

```
ansible-inventory -i ansible/inventory/default_aws_ec2.yaml --list
```

The output:

```
{
    "_meta": {
        "hostvars": {}
    },
    "all": {
        "children": [
            "ungrouped"
        ]
    }
}
```

# Lab 6

## Playbook

```
 ansible-playbook ansible/playbooks/dev/main.yaml --diff
```

The output:

```
PLAY [Prepare docker] ******************************************************************************************************************************************************************************************************************

TASK [docker : include_tasks] **********************************************************************************************************************************************************************************************************
included: /home/irina/PycharmProjects/DevOps_labs/ansible/roles/docker/tasks/install_docker.yml for localhost

TASK [docker : Install Docker packages.] ***********************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [docker : Ensure /etc/docker/ directory exists.] **********************************************************************************************************************************************************************************
skipping: [localhost]

TASK [docker : Configure Docker daemon options.] ***************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [docker : Ensure Docker is started and enabled at boot.] **************************************************************************************************************************************************************************
ok: [localhost]

TASK [docker : include_tasks] **********************************************************************************************************************************************************************************************************
included: /home/irina/PycharmProjects/DevOps_labs/ansible/roles/docker/tasks/install_compose.yml for localhost

TASK [docker : Check current docker-compose version.] **********************************************************************************************************************************************************************************
ok: [localhost]

TASK [docker : set_fact] ***************************************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [docker : Delete existing docker-compose version if it's different.] **************************************************************************************************************************************************************
skipping: [localhost]

TASK [docker : Install docker-compose plugin.] *****************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [docker : Install docker-compose-plugin (with downgrade option).] *****************************************************************************************************************************************************************
skipping: [localhost]

TASK [docker : Ensure handlers are notified now to avoid firewall conflicts.] **********************************************************************************************************************************************************

TASK [docker : Get docker group info using getent.] ************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [web-app : Check if Docker container is running] **********************************************************************************************************************************************************************************
ok: [localhost]

TASK [web-app : Remove Docker container if it is running] ******************************************************************************************************************************************************************************
--- before
+++ after
@@ -1,4 +1,4 @@
 {
-    "exists": true,
-    "running": true
+    "exists": false,
+    "running": false
 }

changed: [localhost]

TASK [web-app : Pull the Docker image from Docker Hub] *********************************************************************************************************************************************************************************
ok: [localhost]

TASK [web-app : Run the Docker container] **********************************************************************************************************************************************************************************************
--- before
+++ after
@@ -1,4 +1,4 @@
 {
-    "exists": false,
-    "running": false
+    "exists": true,
+    "running": true
 }

changed: [localhost]

PLAY RECAP *****************************************************************************************************************************************************************************************************************************
localhost                  : ok=8    changed=2    unreachable=0    failed=0    skipped=8    rescued=0    ignored=0 
```