**Ansilbe Role: pmm-server**
---------------------
Installs and configures pmm-server on RHEL/CentOS or Debian/Ubuntu servers.

----------


**Requirements**


Docker should be installed in the server prior to running this role. Make use of other available docker roles in ansible galaxy before executing this role. Note that this role requires root access, so either run it in a playbook with a global become: yes, or invoke the role in your playbook like:

 

    - hosts: pmm-server
      roles:
        - role: chrissam.pmm-server
          become: yes

----------
**Security Features**

You can protect PMM from unauthorized access using the following security features:

    

 - HTTP password protection adds authentication when accessing the PMM Server web interface

 - SSL encryption secures traffic between PMM Client and PMM Server


----------


**Role Variables**

Available variables are listed below, along with default values (see defaults/main.yml):

    pmm_server_version: 1.0.7

This defines the version of pmm-server that will installed. Percona recommends to use the latest stable version. 


----------


    pmm_server_ENABLE_PROTECTION: true
This defines whether to enable password protection or not. This protects PMM from unauthorized access.


----------


    pmm_server_username: admin
    pmm_server_password: admin
If ENABLE_PROTECTION is set to true then these variables defines the username and password that will be used.


----------

    pmm_server_ENABLE_SSL: true
Enables encryption in  traffic between PMM Client and PMM Server using SSL certificates.


----------

    pmm_server_default_cert: false
If ENABLE_SSL is set to true, then this defines whether a default self-signed certificate should be used.


----------

    pmm_server_certificate_path: ""

If default_cert is set to false then this defines the path where you'll place the custom certificate. The certificate and key name should be "**server.crt** and **server.key**" respectively. Leaving this variable empty will assume that the certificate is placed within the files directory of the role. If specifying a custom path, don't forget to include the trailing slash in the path ( Eg: /path/to/file/ ) and don't include the file name.


----------

    pmm_server_UNINSTALL_PMM: false
Set this to true if you want to uninstall pmm-server. Other variable options will not be considered if this is set to true.

----------
**Possible configuration options**

***Unprotected:*** 

    pmm_server_ENABLE_PROTECTION: false
    pmm_server_ENABLE_SSL: false

***Only password protected:***

    pmm_server_ENABLE_PROTECTION: true
    pmm_server_username: admin
    pmm_server_password: admin

***Only SSL Encryption:***

    pmm_server_ENABLE_SSL: true
    pmm_server_default_cert: true
    (or)
    pmm_server_default_cert: false
    pmm_server_certificate_path: "/path/to/cert/"

***Both password protection and SSL encryption ( Combined Security ):***

    pmm_server_ENABLE_PROTECTION: true
    pmm_server_username: admin
    pmm_server_password: admin
    pmm_server_ENABLE_SSL: true
    pmm_server_default_cert: true
    (or)
    pmm_server_default_cert: false
    pmm_server_certificate_path: "/path/to/cert/"

***Custom options:***

    pmm_server_env_custom:
      METRICS_RETENTION: 192h

----------
**Example Playbook**

    ---
    - hosts: localhost
      become: yes
    
      vars:
        pmm_server_version: 1.0.7
        pmm_server_certificate_path: "~/pmm-certs/"
      
      roles:
        - chrissam.pmm-server

----------


**License**

MIT / BSD


----------
**Author**

This role was created by [Chris Sam](https://linkedin.com/in/chris-sam) for [devopsideas](http://devopsideas.com)



