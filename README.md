### Graph for configuration_injection.yml

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
  Unnamed_task_00_block_start_0-->|Task| write_the_expect_script_to_set_the_local_admin_account0[write the expect script to set the local admin<br>account]:::task
  write_the_expect_script_to_set_the_local_admin_account0-->|Task| give_the_needed_rights_to_execute_the_expect_script1[give the needed rights to execute the expect<br>script]:::task
  give_the_needed_rights_to_execute_the_expect_script1-->|Task| execute_the_expect_script_to_set_up_the_local_admin_account2[execute the expect script to set up the local<br>admin account]:::task
  execute_the_expect_script_to_set_up_the_local_admin_account2-->|Task| generate_the_configuration_for_deployment3[generate the configuration for deployment]:::task
  generate_the_configuration_for_deployment3-->|Task| Apply_the_configuration4[apply the configuration]:::task
  Apply_the_configuration4-->|Task| set_the_SUCCESS_variable_when_the_configuration_are_applied5[set the success variable when the configuration<br>are applied]:::task
  set_the_SUCCESS_variable_when_the_configuration_are_applied5-.->|End of Block| Unnamed_task_00_block_start_0
  set_the_SUCCESS_variable_when_the_configuration_are_applied5-->|Rescue Start| Unnamed_task_00_rescue_start_0[unnamed task 0]:::rescue
  Unnamed_task_00_rescue_start_0-->|Task| set_the_SUCCESS_ariable_whrn_the_config_failed0[set the success ariable whrn the config failed]:::task
  set_the_SUCCESS_ariable_whrn_the_config_failed0-.->|End of Rescue Block| Unnamed_task_00_block_start_0
  set_the_SUCCESS_ariable_whrn_the_config_failed0-->|Block Start| Unnamed_task_11_block_start_0[[unnamed task 1<br>When: **config     ok**]]:::block
  Unnamed_task_11_block_start_0-->|Task| run_show_version_on_remote_devices0[run show version on remote devices]:::task
  run_show_version_on_remote_devices0-.->|End of Block| Unnamed_task_11_block_start_0
  run_show_version_on_remote_devices0-->|Rescue Start| Unnamed_task_11_rescue_start_0[unnamed task 1<br>When: **config     ok**]:::rescue
  Unnamed_task_11_rescue_start_0-->|Task| set_the_SUCCESS_ariable_whrn_the_config_failed0[set the success ariable whrn the config failed]:::task
  set_the_SUCCESS_ariable_whrn_the_config_failed0-.->|End of Rescue Block| Unnamed_task_11_block_start_0
  set_the_SUCCESS_ariable_whrn_the_config_failed0-->End
```


### Graph for reporting.yml

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

  Start-->|Task| Creer_un_dictionnaire_des_informations0[creer un dictionnaire des informations]:::task
  Creer_un_dictionnaire_des_informations0-->|Block Start| Unnamed_task_11_block_start_0[[unnamed task 1]]:::block
  Unnamed_task_11_block_start_0-->|Task| Ecrire_toutes_les_informations_dans_un_seul_fichier0[ecrire toutes les informations dans un seul<br>fichier]:::task
  Ecrire_toutes_les_informations_dans_un_seul_fichier0-->|Task| Lire_le_fichier_ALL_hosts_yml1[lire le fichier all hosts yml]:::task
  Lire_le_fichier_ALL_hosts_yml1-->|Task| Convertir_le_contenu_en_dictionnaire2[convertir le contenu en dictionnaire]:::task
  Convertir_le_contenu_en_dictionnaire2-->|Task| Creer_le_rapport3[creer le rapport]:::task
  Creer_le_rapport3-->|Task| Sending_an_e_mail4[sending an e mail]:::task
  Sending_an_e_mail4-.->|End of Block| Unnamed_task_11_block_start_0
  Sending_an_e_mail4-->End
```


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

  Start-->|Include task| check_deployment_state_yml0[executer les controles pre deploiement<br>include_task: check deployment state yml]:::includeTasks
  check_deployment_state_yml0-->|Include task| configuration_injection_yml1[injection de configuration<br>When: **success     ok**<br>include_task: configuration injection yml]:::includeTasks
  configuration_injection_yml1-->|Include task| reporting_yml2[creation des rapports de fin de script<br>include_task: reporting yml]:::includeTasks
  reporting_yml2-->End
```





## Author Information
your name

#### License

license (GPL-2.0-or-later, MIT, etc)

#### Minimum Ansible Version

2.1

#### Platforms

No platforms specified.
