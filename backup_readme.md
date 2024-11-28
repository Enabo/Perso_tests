<!-- DOCSIBLE START -->

# 📃 Role overview

## backup



Description: your role description


| Field                | Value           |
|--------------------- |-----------------|
| Readme update        | 25/11/2024 |












### Tasks


#### File: tasks/main.yml

| Name | Module | Has Conditions |
| ---- | ------ | --------- |
| prepare the folders needed for the backup, deletes the oldest one and create the one needed for today | block | False |
| set the launch time of the script | set_fact | False |
| Make sure that the working directory exist | ansible.builtin.file | False |
| create the folder name as the current date | ansible.builtin.file | False |
| List all the folder within the working directory | ansible.builtin.find | False |
| Delete the folders that are older than 30 days | ansible.builtin.file | True |
| launch the backup | include_tasks | False |

#### File: tasks/backup_mgt/main.yml

| Name | Module | Has Conditions |
| ---- | ------ | --------- |
| do backup for aruba devices | include_tasks | True |
| load all the vars to the same host | set_fact | False |
| gather all informations from the script to generate and send the report | block | False |
| Create a dictionary for all values of the script | copy | False |
| Get the ALL_host data file | slurp | False |
| Convert the ALL_host data file into a variable | set_fact | False |
| set the repport time | set_fact | False |
| Write the report that will be sent through mail | template | False |
| Sending the mail with the report as content | community.general.mail | False |

#### File: tasks/backup_mgt/aruba.yml

| Name | Module | Has Conditions |
| ---- | ------ | --------- |
| Fetch the running-config for aruba devices | block | False |
| backup the running-config | arubanetworks.aoscx.aoscx_config | False |
| Report non failling arubas | set_fact | False |


## Task Flow Graphs



### Graph for main.yml

```mermaid
flowchart TD
Start
classDef block stroke:#3498db,stroke-width:2px;
classDef task stroke:#4b76bb,stroke-width:2px;
classDef includeTasks stroke:#16a085,stroke-width:2px;
classDef importTasks stroke:#34495e,stroke-width:2px;
classDef includeRole stroke:#2980b9,stroke-width:2px;
classDef importRole stroke:#699ba7,stroke-width:2px;
classDef includeVars stroke:#8e44ad,stroke-width:2px;
classDef rescue stroke:#665352,stroke-width:2px;

  Start-->|Block Start| prepare_the_folders_needed_for_the_backup__deletes_the_oldest_one_and_create_the_one_needed_for_today0_block_start_0[[prepare the folders needed for the backup  deletes<br>the oldest one and create the one needed for today]]:::block
  prepare_the_folders_needed_for_the_backup__deletes_the_oldest_one_and_create_the_one_needed_for_today0_block_start_0-->|Task| set_the_launch_time_of_the_script0[set the launch time of the script]:::task
  set_the_launch_time_of_the_script0-->|Task| Make_sure_that_the_working_directory_exist1[make sure that the working directory exist]:::task
  Make_sure_that_the_working_directory_exist1-->|Task| create_the_folder_name_as_the_current_date2[create the folder name as the current date]:::task
  create_the_folder_name_as_the_current_date2-->|Task| List_all_the_folder_within_the_working_directory3[list all the folder within the working directory]:::task
  List_all_the_folder_within_the_working_directory3-->|Task| Delete_the_folders_that_are_older_than_30_days4[delete the folders that are older than 30 days<br>When: **item path   basename   limit date**]:::task
  Delete_the_folders_that_are_older_than_30_days4-.->|End of Block| prepare_the_folders_needed_for_the_backup__deletes_the_oldest_one_and_create_the_one_needed_for_today0_block_start_0
  Delete_the_folders_that_are_older_than_30_days4-->|Include task| backup_mgt_main_yml1[launch the backup<br>include_task: backup mgt main yml]:::includeTasks
  backup_mgt_main_yml1-->End
```


### Graph for backup_mgt/main.yml

```mermaid
flowchart TD
Start
classDef block stroke:#3498db,stroke-width:2px;
classDef task stroke:#4b76bb,stroke-width:2px;
classDef includeTasks stroke:#16a085,stroke-width:2px;
classDef importTasks stroke:#34495e,stroke-width:2px;
classDef includeRole stroke:#2980b9,stroke-width:2px;
classDef importRole stroke:#699ba7,stroke-width:2px;
classDef includeVars stroke:#8e44ad,stroke-width:2px;
classDef rescue stroke:#665352,stroke-width:2px;

  Start-->|Include task| aruba_yml0[do backup for aruba devices<br>When: **aruba  in group names**<br>include_task: aruba yml]:::includeTasks
  aruba_yml0-->|Task| load_all_the_vars_to_the_same_host1[load all the vars to the same host]:::task
  load_all_the_vars_to_the_same_host1-->|Block Start| gather_all_informations_from_the_script_to_generate_and_send_the_report2_block_start_0[[gather all informations from the script to<br>generate and send the report]]:::block
  gather_all_informations_from_the_script_to_generate_and_send_the_report2_block_start_0-->|Task| Create_a_dictionary_for_all_values_of_the_script0[create a dictionary for all values of the script]:::task
  Create_a_dictionary_for_all_values_of_the_script0-->|Task| Get_the_ALL_host_data_file1[get the all host data file]:::task
  Get_the_ALL_host_data_file1-->|Task| Convert_the_ALL_host_data_file_into_a_variable2[convert the all host data file into a variable]:::task
  Convert_the_ALL_host_data_file_into_a_variable2-->|Task| set_the_repport_time3[set the repport time]:::task
  set_the_repport_time3-->|Task| Write_the_report_that_will_be_sent_through_mail4[write the report that will be sent through mail]:::task
  Write_the_report_that_will_be_sent_through_mail4-->|Task| Sending_the_mail_with_the_report_as_content5[sending the mail with the report as content]:::task
  Sending_the_mail_with_the_report_as_content5-.->|End of Block| gather_all_informations_from_the_script_to_generate_and_send_the_report2_block_start_0
  Sending_the_mail_with_the_report_as_content5-->End
```


### Graph for backup_mgt/aruba.yml

```mermaid
flowchart TD
Start
classDef block stroke:#3498db,stroke-width:2px;
classDef task stroke:#4b76bb,stroke-width:2px;
classDef includeTasks stroke:#16a085,stroke-width:2px;
classDef importTasks stroke:#34495e,stroke-width:2px;
classDef includeRole stroke:#2980b9,stroke-width:2px;
classDef importRole stroke:#699ba7,stroke-width:2px;
classDef includeVars stroke:#8e44ad,stroke-width:2px;
classDef rescue stroke:#665352,stroke-width:2px;

  Start-->|Block Start| Fetch_the_running_config_for_aruba_devices0_block_start_0[[fetch the running config for aruba devices]]:::block
  Fetch_the_running_config_for_aruba_devices0_block_start_0-->|Task| backup_the_running_config0[backup the running config]:::task
  backup_the_running_config0-->|Task| Report_non_failling_arubas1[report non failling arubas]:::task
  Report_non_failling_arubas1-.->|End of Block| Fetch_the_running_config_for_aruba_devices0_block_start_0
  Report_non_failling_arubas1-->|Rescue Start| Fetch_the_running_config_for_aruba_devices0_rescue_start_0[fetch the running config for aruba devices]:::rescue
  Fetch_the_running_config_for_aruba_devices0_rescue_start_0-->|Task| Report_failing_arubas0[report failing arubas]:::task
  Report_failing_arubas0-.->|End of Rescue Block| Fetch_the_running_config_for_aruba_devices0_block_start_0
  Report_failing_arubas0-->End
```


## Playbook

```yml
---
- name: Playbook for network and cybersecurity devices running-configuration backup
  hosts: aruba
  gather_facts: no
  vars:
    working_dir: tmp/backup
    current_date: "{{ lookup('pipe', 'date +\"%Y_%m_%d\"') }}"
    limit_date: "{{ lookup('pipe', 'date --date=\"30 days ago\" +%Y_%m_%d') }}"
  roles:
    - backup

```
## Playbook graph
```mermaid
flowchart TD
  aruba-->|Role| backup[backup]
```

## Author Information
your name

#### License

license (GPL-2.0-or-later, MIT, etc)

#### Minimum Ansible Version

2.1

#### Platforms

No platforms specified.
<!-- DOCSIBLE END -->[
