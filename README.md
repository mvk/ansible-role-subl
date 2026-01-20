<!-- DOCSIBLE START -->
# 📃 Role overview

## mvk.subl



Description: Install Sublime Text editor










### Defaults

**These are static variables with lower priority**

#### File: defaults/main.yml

| Var          | Type         | Value       |
|--------------|--------------|-------------|
| [mvk_subl_release](defaults/main.yml#L4)   | str | `stable` |    
| [mvk_subl_server](defaults/main.yml#L5)   | str | `https://download.sublimetext.com` |    
| [mvk_subl_dnf_package](defaults/main.yml#L6)   | str | `sublime-text` |    
| [mvk_subl_dnf_key](defaults/main.yml#L7)   | str | `sublimehq-rpm-pub.gpg` |    
| [mvk_subl_dnf_repo](defaults/main.yml#L8)   | str | `rpm/{{ mvk_subl_release }}/{{ ansible_architecture }}/{{ mvk_subl_dnf_package }}.repo` |    
| [mvk_subl_apt_key](defaults/main.yml#L11)   | str | `sublimehq-pub.gpg` |    
| [mvk_subl_apt_key_path](defaults/main.yml#L12)   | str | `/etc/apt/keyrings/sublimehq-pub.asc` |    
| [mvk_subl_apt_repo_path](defaults/main.yml#L13)   | str | `etc/apt/sources.list.d/{{ mvk_subl_dnf_package }}.sources` |    
| [mvk_subl_packages](defaults/main.yml#L16)   | list | `[]` |    
| [mvk_subl_packages.**0**](defaults/main.yml#L17)   | str | `A File Icon` |    
| [mvk_subl_packages.**1**](defaults/main.yml#L18)   | str | `Emmet` |    
| [mvk_subl_packages.**2**](defaults/main.yml#L19)   | str | `SideBarEnhancements` |    
| [mvk_subl_packages.**3**](defaults/main.yml#L20)   | str | `Terminus` |    
| [mvk_subl_packages.**4**](defaults/main.yml#L21)   | str | `GitGutter` |    
| [mvk_subl_packages.**5**](defaults/main.yml#L22)   | str | `Jinja2` |    
| [mvk_subl_packages.**6**](defaults/main.yml#L23)   | str | `Ansible` |    
| [mvk_subl_packages.**7**](defaults/main.yml#L24)   | str | `Ansible Vault` |    
| [mvk_subl_license](defaults/main.yml#L24)   | str |  |    





### Tasks


#### File: tasks/apt/install.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Import gpg public key | ansible.builtin.get_url | False |
| Create repository sources file | ansible.builtin.template | False |
| Install package sublime-text | ansible.builtin.apt | False |

#### File: tasks/dnf5/install.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Import gpg public key | ansible.builtin.shell | False |
| Create repository config file | ansible.builtin.shell | False |
| Setup regex guard variables | ansible.builtin.set_fact | False |
| Attempt to dnf install the package sublime-text | ansible.builtin.dnf | False |
| Handle missing digest installation | ansible.builtin.include_tasks | True |

#### File: tasks/dnf5/install_workaround_no_digest.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Download locall the package sublime-text | ansible.builtin.command | False |
| Find the RPM file for sublime-text | ansible.builtin.find | False |
| Fail if we haven't found exactly 1 file | ansible.builtin.fail | True |
| Force install RPM ignoring file and contents digests | ansible.builtin.shell | False |

#### File: tasks/license.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Ensure Sublime Text Local directory exists | ansible.builtin.file | False |
| Deploy Sublime Text License | ansible.builtin.copy | False |

#### File: tasks/main.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Install sublime for package manager {{ ansible_pkg_mgr }} | ansible.builtin.include_tasks | False |
| Install sublime Package Control | ansible.builtin.include_tasks | False |
| Install sublime packages | ansible.builtin.include_tasks | True |
| Install sublime license is mvk_subl_license is set | ansible.builtin.include_tasks | True |

#### File: tasks/package-control.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Calculate install_dir | ansible.builtin.set_fact | False |
| Create install_dir | ansible.builtin.file | False |
| Download Package Control package | ansible.builtin.get_url | False |

#### File: tasks/packages.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Ensure Sublime Text User directory exists | ansible.builtin.file | False |
| Deploy Package Control settings | ansible.builtin.copy | False |


## Task Flow Graphs



### Graph for apt/install.yml

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

  Start-->|Task| Import_gpg_public_key0[import gpg public key]:::task
  Import_gpg_public_key0-->|Task| Create_repository_sources_file1[create repository sources file]:::task
  Create_repository_sources_file1-->|Task| Install_package_sublime_text2[install package sublime text]:::task
  Install_package_sublime_text2-->End
```


### Graph for dnf5/install.yml

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

  Start-->|Task| Import_gpg_public_key0[import gpg public key]:::task
  Import_gpg_public_key0-->|Task| Create_repository_config_file1[create repository config file]:::task
  Create_repository_config_file1-->|Task| Setup_regex_guard_variables2[setup regex guard variables]:::task
  Setup_regex_guard_variables2-->|Task| Attempt_to_dnf_install_the_package_sublime_text3[attempt to dnf install the package sublime text]:::task
  Attempt_to_dnf_install_the_package_sublime_text3-->|Include task| Handle_missing_digest_installation_dnf5_install_workaround_no_digest_yml_4[handle missing digest installation<br>When: **initial dnf install rc   default 0     0 and<br>initial dnf install failures   default      <br>select  match   regex str    list   length   0**<br>include_task: dnf5 install workaround no digest yml]:::includeTasks
  Handle_missing_digest_installation_dnf5_install_workaround_no_digest_yml_4-->End
```


### Graph for dnf5/install_workaround_no_digest.yml

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

  Start-->|Task| Download_locall_the_package_sublime_text0[download locall the package sublime text]:::task
  Download_locall_the_package_sublime_text0-->|Task| Find_the_RPM_file_for_sublime_text1[find the rpm file for sublime text]:::task
  Find_the_RPM_file_for_sublime_text1-->|Task| Fail_if_we_haven_t_found_exactly_1_file2[fail if we haven t found exactly 1 file<br>When: **found files files   default       length    1**]:::task
  Fail_if_we_haven_t_found_exactly_1_file2-->|Task| Force_install_RPM_ignoring_file_and_contents_digests3[force install rpm ignoring file and contents<br>digests]:::task
  Force_install_RPM_ignoring_file_and_contents_digests3-->End
```


### Graph for license.yml

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

  Start-->|Task| Ensure_Sublime_Text_Local_directory_exists0[ensure sublime text local directory exists]:::task
  Ensure_Sublime_Text_Local_directory_exists0-->|Task| Deploy_Sublime_Text_License1[deploy sublime text license]:::task
  Deploy_Sublime_Text_License1-->End
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

  Start-->|Include task| Install_sublime_for_package_manager_ansible_pkg_mgr____ansible_pkg_mgr____install_yml_0[install sublime for package manager ansible pkg<br>mgr<br>include_task:    ansible pkg mgr    install yml]:::includeTasks
  Install_sublime_for_package_manager_ansible_pkg_mgr____ansible_pkg_mgr____install_yml_0-->|Include task| Install_sublime_Package_Control_package_control_yml_1[install sublime package control<br>include_task: package control yml]:::includeTasks
  Install_sublime_Package_Control_package_control_yml_1-->|Include task| Install_sublime_packages_packages_yml_2[install sublime packages<br>When: **mvk subl packages   default       length   0**<br>include_task: packages yml]:::includeTasks
  Install_sublime_packages_packages_yml_2-->|Include task| Install_sublime_license_is_mvk_subl_license_is_set_license_yml_3[install sublime license is mvk subl license is set<br>When: **mvk subl license   default       length   0**<br>include_task: license yml]:::includeTasks
  Install_sublime_license_is_mvk_subl_license_is_set_license_yml_3-->End
```


### Graph for package-control.yml

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

  Start-->|Task| Calculate_install_dir0[calculate install dir]:::task
  Calculate_install_dir0-->|Task| Create_install_dir1[create install dir]:::task
  Create_install_dir1-->|Task| Download_Package_Control_package2[download package control package]:::task
  Download_Package_Control_package2-->End
```


### Graph for packages.yml

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

  Start-->|Task| Ensure_Sublime_Text_User_directory_exists0[ensure sublime text user directory exists]:::task
  Ensure_Sublime_Text_User_directory_exists0-->|Task| Deploy_Package_Control_settings1[deploy package control settings]:::task
  Deploy_Package_Control_settings1-->End
```





## Author Information
Max Kovgan

#### License

MIT

#### Minimum Ansible Version

2.1

#### Platforms

- **Fedora**: ['42', '43']
- **Debian**: ['bookworm', 'bullseye']
- **Ubuntu**: ['noble', 'plucky', 'questing']


#### Dependencies

No dependencies specified.
<!-- DOCSIBLE END -->
