role-mysql
================

Installs an MSSQL Database Engine and optional the SQL Management Studio on a Windows Server
optionally sets up databases and permissions

Requirements
---------------

Ansible >= 2.7.x
Windows Server from 2012R2
MSSQL Server install ISO version >= 2014
SSMS EXE install package

Source (ISO Packages) should be in place. 


Variables
----------------
```
- rl_mssql_temp_folder: sets a folder for the downloads and temps 

- rl_mssql_install_ssms: do you want to install the SSMS? (default: false)

- rl_mssql_iso_source: defines the ISO Download details
  - name: name of the ISO
    repo: name of the repo
    productkey: defines the product key (default: unset)
    
rl_mssql_ssms_source: defines the SSMS install package Download details
  - name: name of the executable (default: SSMS-Setup-ENU.exe )
    repo: download path
    product_id: the (windows) product ID of the version

rl_mssql_instances: defines the instances to setup, multible instances are possible (default: MSSQLSERVER )
  - instance_name: MSSQLSERVER
    features: SQLENGINE
    instance_collation: SQL_Latin1_General_CP1_CI_AS
    sysadmins: 
      - "{{ inventory_hostname_short }}\\{{ ansible_user }}"
    sqlusers: 
      - "{{ inventory_hostname_short }}\\{{ ansible_user }}"
    setupadmins: 
      - "{{ inventory_hostname_short }}\\{{ ansible_user }}"
    svcaccount: "{{ inventory_hostname_short }}\\{{ ansible_user }}"
    svcpassword: "{{ ansible_password }}"
    instance_dir: C:\Program Files\Microsoft SQL Server
    installdb_path: C:\Program Files\Microsoft SQL Server\MSSQLSERVER\MSSQL\Data
    userldb_path: C:\Program Files\Microsoft SQL Server\MSSQLSERVER\MSSQL\Data
    userdblog_path: C:\Program Files\Microsoft SQL Server\MSSQLSERVER\MSSQL\Data
    tempdb_path: C:\Program Files\Microsoft SQL Server\MSSQLSERVER\MSSQL\Data
    tempdblog_path: C:\Program Files\Microsoft SQL Server\MSSQLSERVER\MSSQL\Data
    backup_path: C:\Program Files\Microsoft SQL Server\MSSQLSERVER\MSSQL\Backup
    databases: 
      - rl_mssql_db
```

Dependencies
--------------

no direct dependencies. the role downloads the DSC Modules. 
Download paths are needed.

Example Playbook
----------------

eg:

```
    - name: Install MSSQL
      hosts: localhost

      tasks: 
      - import_role: role-mssql
        vars:
          rl_mssql_install_ssms: true
         
```


License
-------

MIT

Author Information
------------------

David Surey <git@digitalismus.org>