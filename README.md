# redops.lampstack #

RedOps Lamp Stack with optional multiple php version provisioning

Role Variables
--------------
 - ServerName (Domain Name System) of the target website
 - ServerAdmin (Server Administrator Email address)
 - ServerAlias (Server Alias for example for www.domain.com)
 - DocumentRoot (Document Root Location: Location of a php website files)
 - php_version (PHP Version to be use for example: php7.2) Valid values are "5.6" "7.0" "7.1" "7.2" "7.3" "7.4" multi_php should not be defined when using php specific version
 - multi_php (If you want to install multiple php versions in one lamp) Note: php_version variable must be unset.

Example Playbook
----------------
Example Playbook for lamp stack provisioning:

    - hosts: Ubuntu_Server_Focal
      gather_facts: yes
      become: yes
      vars:
        ServerName: goadminops.com
        ServerAdmin: alfred98valderrama@gmail.com
        ServerAlias: www.goadminops.com
        DocumentRoot: /var/www/goadminops.com
        # multi_php: true # (Optional)
        php_version: "7.3" # Comment-out when multi_php variable is set to true
        mysql_enabled_on_startup: true
        mysql_packages:
          - mysql-server
          - mysql-client
        mysql_root_password: "verystrongpassword"
        mysql_databases:
          - name: "laravel"
        mysql_users:
          - name: "laravel"
            host: "%"
            password: "verystrongpassword"
            priv: "laravel.*:ALL"
      roles:
         - redops.lampstack
         - geerlingguy.mysql
      ignore_errors: '{{ ansible_check_mode }}'
      
License
-------

BSD

Author Information
------------------

- Name: Alfred Valderrama
- Email: alfred98valderrama@gmail.com
- Github Repository: https://github.com/redopsbay
- Website: https://goadminops.com
