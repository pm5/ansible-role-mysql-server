mysql-server
============

[![Build Status](https://travis-ci.org/infOpen/ansible-role-mysql-server.svg?branch=master)](https://travis-ci.org/infOpen/ansible-role-mysql-server)

Install mysql-server package.

Requirements
------------

This role requires Ansible 1.4 or higher, and platform requirements are listed
in the metadata file.

Role Variables
--------------

Follow the possible variables with their default values

    # Defaults file for mysql-server

    # Package variables
    #------------------
    mysqlserver_package_state : present

    # Service variables
    #------------------
    mysqlserver_service_state   : started
    mysqlserver_service_enabled : True

    mysqlserver_managed_by_phpmyadmin : False

    mysqlserver_owner : mysql
    mysqlserver_group : mysql

    #===============================================================================
    # Credentials
    #===============================================================================

    mysqlserver_root_db_password     : ""
    mysqlserver_root_db_old_password : ""

    mysqlserver_global_accounts      : []
    mysqlserver_additionnal_accounts : []

    #===============================================================================
    # First used for config files
    #===============================================================================

    # Client
    mysqlserver_client_port   : 3306
    mysqlserver_client_socket : "/var/run/mysqld/mysqld.sock"


    # mysqld_safe
    mysqlserver_mysqld_safe_socket : "/var/run/mysqld/mysqld.sock"
    mysqlserver_mysqld_safe_nice   : 0


    # mysqld
    mysqlserver_mysqld_user            : mysql
    mysqlserver_mysqld_pid_file        : /var/run/mysqld/mysqld.pid
    mysqlserver_mysqld_socket          : /var/run/mysqld/mysqld.sock
    mysqlserver_mysqld_port            : 3306
    mysqlserver_mysqld_basedir         : /usr
    mysqlserver_mysqld_datadir         : /var/lib/mysql
    mysqlserver_mysqld_tmpdir          : /tmp
    mysqlserver_mysqld_lc_messages_dir : /usr/share/mysql

    mysqlserver_mysqld_skip_external_locking : True

    mysqlserver_mysqld_bind_address : 127.0.0.1

    mysqlserver_mysqld_key_buffer          : 16M
    mysqlserver_mysqld_max_allowed_packet  : 16M
    mysqlserver_mysqld_thread_stack        : 192K
    mysqlserver_mysqld_thread_cache_size   : 8

    mysqlserver_mysqld_myisam_recover_options : BACKUP
    mysqlserver_mysqld_max_connections        : 100
    mysqlserver_mysqld_table_cache            : 64
    mysqlserver_mysqld_thread_concurrency     : 10

    mysqlserver_mysqld_query_cache_limit   : 1M
    mysqlserver_mysqld_query_cache_size    : 16M

    mysqlserver_mysqld_general_log_file    : /var/log/mysql/mysql.log
    mysqlserver_mysqld_general_log         : 1
    mysqlserver_mysqld_log_error           : /var/log/mysql/error.log
    mysqlserver_mysqld_slow_query_log_file : /var/log/mysql/mysql-slow.log
    mysqlserver_mysqld_slow_query_log      : 1
    mysqlserver_mysqld_long_query_time     : 2
    mysqlserver_mysqld_log_queries_not_using_indexes : True

    mysqlserver_mysqld_server_id           : 1
    mysqlserver_mysqld_log_bin             : /var/log/mysql/mysql-bin.log
    mysqlserver_mysqld_expire_logs_days    : 10
    mysqlserver_mysqld_max_binlog_size     : 100M
    mysqlserver_mysqld_binlog_do_db        : include_database_name
    mysqlserver_mysqld_binlog_ignore_db    : include_database_name
    mysqlserver_mysqld_binlog_format       : mixed

    # mysqldump
    mysqlserver_mysqldump_quick              : True
    mysqlserver_mysqldump_quote_names        : True
    mysqlserver_mysqldump_max_allowed_packet : 16M

    # mysql
    mysqlserver_mysql_no_auto_rehash : False

    # isamchk
    mysqlserver_isamchk_key_buffer : 16M


Specific OS family vars :

    # Debian vars
    mysqlserver_packages :
      - mysql-client
      - mysql-common
      - mysql-server
      - mysql-server-core
      - python-mysqldb

    mysqlserver_service_name : mysql

    mysqlserver_config_file_location : "/etc/mysql/my.cnf"


Syntax for user creation :

    mysqlserver_global_accounts :

      # Monitoring account
      - name       : monitoring
        password   : foobar
        host       : localhost
        state      : present
        files      :
          - path  : "/root/.my_monitoring.cnf"
            owner : root
            group : root
            mode  : 0400
        privileges :
          - "*.*:USAGE"


Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: achaussier.mysql-server }

License
-------

MIT

Author Information
------------------

Alexandre Chaussier (for Infopen company)
- http://www.infopen.pro
- a.chaussier [at] infopen.pro
