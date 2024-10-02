# role-aap-object-credential
Ansible role to build AAP schedule objects

# Ref
https://console.redhat.com/ansible/automation-hub/repo/published/ansible/controller/content/module/schedule/


# How to use

Step 1: Install the role in your environment.
   - You could have roles/requirements.yml if running on AAP.
   - Or simple install on your environment.

Step 2: Define your variables

- Role takes in a list of values that define a single schedule

build: true/false # Bool value to switch role on off.

list_name:
  - schedule name
  - job template name
  - description 
  - rrule

Step 3: Call the role from your playbook.

# Example

## varible definition in group_vars/*.yml
example-vars.yml
  
##
example-playbook.yml
