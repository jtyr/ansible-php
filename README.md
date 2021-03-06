php
===

Ansible role which helps to install and configure PHP and PHP extensions.

The configuration of the role is done in such way that it should not be
necessary to change the role for any kind of configuration. All can be
done either by changing role parameters or by declaring completely new
configuration as a variable. That makes this role absolutely
universal. See the examples below for more details.

Please report any issues or send PR.


Examples
--------

```yaml
---

# Example of how to use the role with default parameters
- hosts: myhost1
  roles:
    - php

# Example of how to configure a PHP extension
- hosts: myhost2
  vars:
    php_extensions_config:
      zabbix:
        # This actually overrides the php.ini configuration
        PHP:
          post_max_size: 16M
          max_execution_time: 300
          max_input_time: 300
        date:
          date.timezone: UTC
  roles:
    - php
```


Role variables
--------------

Variables used by the role is as follows:

```yaml
# Whether to install EPEL YUM repo
php_epel_yumrepo_install: "{{ yumrepo_epel_install | default(false) }}"

# EPEL YUM repo URL
php_epel_yumrepo_url: "{{ yumrepo_epel_url | default('https://dl.fedoraproject.org/pub/epel/$releasever/$basearch/') }}"

# EPEL YUM repo GPG key
php_epel_yumrepo_gpgkey: "{{ yumrepo_epel_gpgkey | default('https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-$releasever') }}"

# Additional EPEL params
php_epel_yumrepo_params: "{{ yumrepo_epel_params | default({}) }}"

# Whether to install the SCL YUM repo
php_scl_yumrepo_install: no

# SCL YUM repo URL
php_scl_yumrepo_url: http://mirror.centos.org/centos/$releasever/sclo/$basearch/rh/

# Additional SCL YUM repo params
php_scl_yumrepo_params: {}

# Package to be installed (explicit version can be specified here)
php_pkg: php

# Exptensions prefix (set it to null to use no prefix)
php_extensions_prefix: php

# Extensions packages to be installed
php_extensions_pkgs: []
# Example:
#php_extensions_pkgs:
#  - gd
#  - xml

# Default path to the php.ini file
php_config_file: /etc/php.ini

# Default path to the php.d directory
php_config_dir: /etc/php.d

# Default php.ini config (will be skipped if set to null)
php_config: null
# Example:
#php_config:
#  PHP:
#    engine: "On"
#    short_open_tag: "Off"
#    asp_tags: "Off"
#    precision: 14
#    y2k_compliance: "On"
#    output_buffering: 4096
#    zlib.output_compression: "Off"
#    implicit_flush: "Off"
#    unserialize_callback_func: ""
#    serialize_precision: 100
#    allow_call_time_pass_reference: "Off"
#    safe_mode: "Off"
#    safe_mode_gid: "Off"
#    safe_mode_include_dir: ""
#    safe_mode_exec_dir: ""
#    safe_mode_allowed_env_vars: PHP_
#    safe_mode_protected_env_vars: LD_LIBRARY_PATH
#    disable_functions: ""
#    disable_classes: ""
#    expose_php: "On"
#    max_execution_time: 30
#    max_input_time: 60
#    memory_limit: 128M
#    error_reporting: E_ALL & ~E_DEPRECATED
#    display_errors: "Off"
#    display_startup_errors: "Off"
#    log_errors: "On"
#    log_errors_max_len: 1024
#    ignore_repeated_errors: "Off"
#    ignore_repeated_source: "Off"
#    report_memleaks: "On"
#    track_errors: "Off"
#    html_errors: "Off"
#    variables_order: GPCS
#    request_order: GP
#    register_globals: "Off"
#    register_long_arrays: "Off"
#    register_argc_argv: "Off"
#    auto_globals_jit: "On"
#    post_max_size: 8M
#    magic_quotes_gpc: "Off"
#    magic_quotes_runtime: "Off"
#    magic_quotes_sybase: "Off"
#    auto_prepend_file: ""
#    auto_append_file: ""
#    default_mimetype: text/html
#    doc_root: ""
#    user_dir: ""
#    enable_dl: "Off"
#    file_uploads: "On"
#    upload_max_filesize: 2M
#    allow_url_fopen: "On"
#    allow_url_include: "Off"
#    default_socket_timeout: 60
#  Date: {}
#  filter: {}
#  iconv: {}
#  intl: {}
#  sqlite: {}
#  sqlite3: {}
#  Pcre: {}
#  Pdo: {}
#  Phar: {}
#  Syslog:
#    define_syslog_variables: "Off"
#  mail function:
#    SMTP: localhost
#    smtp_port: 25
#    sendmail_path: /usr/sbin/sendmail -t -i
#    mail.add_x_header: "On"
#  SQL:
#    sql.safe_mode: "Off"
#  ODBC:
#    odbc.allow_persistent: "On"
#    odbc.check_persistent: "On"
#    odbc.max_persistent: -1
#    odbc.max_links: -1
#    odbc.defaultlrl: 4096
#    odbc.defaultbinmode: 1
#  MySQL:
#    mysql.allow_persistent: "On"
#    mysql.max_persistent: -1
#    mysql.max_links: -1
#    mysql.default_port: ""
#    mysql.default_socket: ""
#    mysql.default_host: ""
#    mysql.default_user: ""
#    mysql.default_password: ""
#    mysql.connect_timeout: 60
#    mysql.trace_mode: "Off"
#  MySQLi:
#    mysqli.max_links: -1
#    mysqli.default_port: 3306
#    mysqli.default_socket: ""
#    mysqli.default_host: ""
#    mysqli.default_user: ""
#    mysqli.default_pw: ""
#    mysqli.reconnect: "Off"
#  PostgresSQL:
#    pgsql.allow_persistent: "On"
#    pgsql.auto_reset_persistent: "Off"
#    pgsql.max_persistent: -1
#    pgsql.max_links: -1
#    pgsql.ignore_notice: 0
#    pgsql.log_notice: 0
#  Sybase-CT:
#    sybct.allow_persistent: "On"
#    sybct.max_persistent: -1
#    sybct.max_links: -1
#    sybct.min_server_severity: 10
#    sybct.min_client_severity: 10
#  bcmath:
#    bcmath.scale: 0
#  browscap: {}
#  Session:
#    session.save_handler: files
#    session.save_path: /var/lib/php/session
#    session.use_cookies: 1
#    session.use_only_cookies: 1
#    session.name: PHPSESSID
#    session.auto_start: 0
#    session.cookie_lifetime: 0
#    session.cookie_path: /
#    session.cookie_domain: ""
#    session.cookie_httponly: ""
#    session.serialize_handler: php
#    session.gc_probability: 1
#    session.gc_divisor: 1000
#    session.gc_maxlifetime: 1440
#    session.bug_compat_42: "Off"
#    session.bug_compat_warn: "Off"
#    session.referer_check: ""
#    session.entropy_length: 0
#    session.entropy_file: ""
#    session.cache_limiter: nocache
#    session.cache_expire: 180
#    session.use_trans_sid: 0
#    session.hash_function: 0
#    session.hash_bits_per_character: 5
#    url_rewriter.tags: "a: href,area: href,frame: src,input: src,form: fakeentry"
#  MSSQL:
#    mssql.allow_persistent: "On"
#    mssql.max_persistent: -1
#    mssql.max_links: -1
#    mssql.min_error_severity: 10
#    mssql.min_message_severity: 10
#    mssql.compatability_mode: "Off"
#    mssql.secure_connection: "Off"
#  Assertion: {}
#  COM: {}
#  mbstring: {}
#  gd: {}
#  exif: {}
#  Tidy:
#    tidy.clean_output: "Off"
#  soap:
#    soap.wsdl_cache_enabled: 1
#    soap.wsdl_cache_dir: /tmp
#    soap.wsdl_cache_ttl: 86400
#  sysvshm: {}

# Extensions configurations
php_extensions_config: {}
# Example:
#php_extensions_config:
#  gd:
#    extension: gd.so
#  xmlreader:
#    extension: xmlreader.so
#  xmlwriter:
#    extension: xmlwriterr.so
```


Dependencies
------------

- [`config_encoder_filters`](https://github.com/jtyr/ansible-config_encoder_filters)
- [`php_fpm`](https://github.com/jtyr/ansible-php_fpm) role (optional)


License
-------

MIT


Author
------

Jiri Tyr
