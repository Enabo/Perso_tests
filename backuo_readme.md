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
| Unnamed_block | block | False |
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
| Unnamed_block | block | False |
| Lire le fichier ALL_hosts.yml | slurp | False |
| Convertir le contenu en dictionnaire | set_fact | False |
| set the repport time | set_fact | False |
| Creer le rapport | template | False |
| Sending an e-mail | community.general.mail | False |

#### File: tasks/backup_mgt/aruba.yml

| Name | Module | Has Conditions |
| ---- | ------ | --------- |
| Unnamed_block | block | False |
| Check ssh port |  | False |
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

  Start-->|Block Start| Unnamed_task_00_block_start_0[[unnamed task 0]]:::block
  Unnamed_task_00_block_start_0-->|Task| set_the_launch_time_of_the_script0[set the launch time of the script]:::task
  set_the_launch_time_of_the_script0-->|Task| Make_sure_that_the_working_directory_exist1[make sure that the working directory exist]:::task
  Make_sure_that_the_working_directory_exist1-->|Task| create_the_folder_name_as_the_current_date2[create the folder name as the current date]:::task
  create_the_folder_name_as_the_current_date2-->|Task| List_all_the_folder_within_the_working_directory3[list all the folder within the working directory]:::task
  List_all_the_folder_within_the_working_directory3-->|Task| Delete_the_folders_that_are_older_than_30_days4[delete the folders that are older than 30 days<br>When: **item path   basename   limit date**]:::task
  Delete_the_folders_that_are_older_than_30_days4-.->|End of Block| Unnamed_task_00_block_start_0
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
  load_all_the_vars_to_the_same_host1-->|Block Start| Unnamed_task_22_block_start_0[[unnamed task 2]]:::block
  Unnamed_task_22_block_start_0-->|Task| Lire_le_fichier_ALL_hosts_yml0[lire le fichier all hosts yml]:::task
  Lire_le_fichier_ALL_hosts_yml0-->|Task| Convertir_le_contenu_en_dictionnaire1[convertir le contenu en dictionnaire]:::task
  Convertir_le_contenu_en_dictionnaire1-->|Task| set_the_repport_time2[set the repport time]:::task
  set_the_repport_time2-->|Task| Creer_le_rapport3[creer le rapport]:::task
  Creer_le_rapport3-->|Task| Sending_an_e_mail4[sending an e mail]:::task
  Sending_an_e_mail4-.->|End of Block| Unnamed_task_22_block_start_0
  Sending_an_e_mail4-->End
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

  Start-->|Block Start| Unnamed_task_00_block_start_0[[unnamed task 0]]:::block
  Unnamed_task_00_block_start_0-->|Task| Check_ssh_port0[check ssh port]:::task
  Check_ssh_port0-->|Task| Report_non_failling_arubas1[report non failling arubas]:::task
  Report_non_failling_arubas1-.->|End of Block| Unnamed_task_00_block_start_0
  Report_non_failling_arubas1-->|Rescue Start| Unnamed_task_00_rescue_start_0[unnamed task 0]:::rescue
  Unnamed_task_00_rescue_start_0-->|Task| Report_failing_arubas0[report failing arubas]:::task
  Report_failing_arubas0-.->|End of Rescue Block| Unnamed_task_00_block_start_0
  Report_failing_arubas0-->End
```


## Playbook

```yml
---
- name: Playbook for network and cybersecurity running-configuration backup
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
