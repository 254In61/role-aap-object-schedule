# role-aap-object-credential
Ansible role to build AAP schedule objects

# Ref
https://console.redhat.com/ansible/automation-hub/repo/published/ansible/controller/content/module/schedule/


# How to use

Step 1: Install the role in your environment.
   - You could have roles/requirements.yml if running on AAP.
   - Or simple install on your environment.

Step 2: Define your variables

schedule: true/false # Bool value to switch role on off.

list_name:
  - schedule name
  - job template name
  - description 
  - rrule

Step 3: Call the role from your playbook.

# Example

## varible definition in group_vars/*.yml
cisco_schedule:
  - "{{ cisco_config_backup_job_template_name }}" # re-using job-template name
  - "{{ cisco_config_backup_job_template_name }}"
  - "{{ common_description }}"
  - "DTSTART;TZID={{ time_zone }}:{{ start_date }}T{{ cisco_schedule_run_time }}00 RRULE:FREQ={{ frequency }};INTERVAL={{ interval }}"
  

junos_schedule:
  - "{{ junos_config_backup_job_template_name }}" # re-using job-template name
  - "{{ junos_config_backup_job_template_name }}"
  - "{{ common_description }}"
  - "DTSTART;TZID={{ time_zone }}:{{ start_date }}T{{ junos_schedule_run_time }}00 RRULE:FREQ={{ frequency }};INTERVAL={{ interval }}"
  

  
##

---
- name: Playbook to configure AAP
  hosts: localhost
  gather_facts: false
 
  pre_tasks:
    - name: Include specific project variables
      ansible.builtin.include_vars:
        dir: group_vars

  tasks:
    !
    !
    - name: Import role-aap-object-schedule
      ansible.builtin.include_role:
        name: role-aap-object-schedule
      vars:
        schedule: true
        in_list: "{{ item }}"
      loop:
        - "{{ cisco_schedule }}"
        - "{{ junos_schedule }}"
    !
    !