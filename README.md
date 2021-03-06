freebsd-jailed
=========

This role provides just a jail. Nothing more. Is used by other roles to created jailed serices. The package `ssmtp` is installed and preconfigured as well if requested (define `use_ssmtp`). Furthermore syslogd is configured to forward all messsages to a central syslogd server if wanted (define `use_syslogd_server`).

To see this role in action, have a look at [this project of mine](https://github.com/JoergFiedler/freebsd-ansible-demo).

Requirements
------------

This role is intent to be used with a fresh FreeBSD 10.2 installation. There is a Vagrant Box with providers for VirtualBox and EC2 you may use.

You will find a sample project which uses this role [here](https://github.com/JoergFiedler/freebsd-ansible-demo).

Role Variables
--------------

##### jail_name

The name for the jail. Local part of the hostname. Default: `'{{ jail_net_ip }}'`.

##### jail_domain

The domain this jail belongs to. Domain part of the hostname. Default: `'darkcity'`.

##### jail_net_if

The interface to which the jail's ip address is added. Default: `'lo0'`.

##### jail_net_ip

The jail's ip address. No default value.

##### syslogd_server

The syslogd server to which all syslog messages are going to be forwarded. No default value.

This feature is only active if the variable `use_syslogd_server` is set to any value.

##### host_build_server_enabled

Use own build server repositry to install customized build ports. Default: `'yes'`

##### host_build_server_url

The build server repo http url. Default: `'https://s3-eu-west-1.amazonaws.com/vastland.moumantai.de/public/FreeBSD/packages/freebsd-10_2_x64-HEAD'`

##### host_build_server_pubkey

The public key to use to verify signatures. Default: `'poudriere.pub'`

Dependencies
------------

- [JoergFiedler.freebsd-jail-host](https://galaxy.ansible.com/detail#/role/5827)

Example Playbook
----------------

    - { role: JoergFiedler.freebsd-jailed-syslogd,
        use_ssmtp: true,
        use_syslogd_server: true,
        syslogd_server: '10.1.0.99',
        jail_name: 'dummy',
        jail_net_ip: '10.1.0.2' }

License
-------

BSD

Author Information
------------------

If you like it or do have ideas to improve this project, please open an issue on Github. Thanks.
