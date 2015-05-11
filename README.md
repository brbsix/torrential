# torrential

`torrential` is a shell script used to check and manipulate firewall rules for an application. It was designed to quickly change firewall application rules on-demand for use with BitTorrent. It can be used to quickly check the state of the firewall (enabled/disabled), status of application rules (ALLOW/DENY), set rules to ALLOW, and set rules to DENY.

`torrential-wrapper` is used to open up your BitTorrent client of choice. Upon execution, firewall application rules are set to ALLOW and the BitTorrent client is started. Upon termination of the client, the firewall application rules are set to DENY.

Installation
------------

`torrential` is configured by default to use *transmission* as the default UFW app profile and/or the port 51413. You should edit the global variables for the aforementioned items if you will be using other values. The script will attempt to use the app profile by default - if it does not exist, it will use the port number instead.

`torrential-wrapper` is configured by default to launch `transmission-gtk`. You should change it if you'd like to use another BitTorrent client instead.

To install `torrential` and `torrential-wrapper`:

    sudo install torrential torrential-wrapper /usr/local/bin

Root access is required by `torrential` in order to function. In order to use it without interruption, it is strongly recommended to install a sudoers file. This allows the `torrential-wrapper` to call `sudo torrential` without prompt.

You will need to edit *sudoers* prior to installation. Replace USERNAME and HOSTNAME with your respective values. Also, update the path to `torrential` if you will be installing it in a location other than */usr/local/bin*. To install the sudoers file:

    sudo install -m 0440 sudoers /etc/sudoers.d/torrential

Requirements
------------

`torrential` is only compatible with UFW, a frontend for iptables dubbed "The Uncomplicated FireWall".

It also requires **lockfile-progs**, generally available via `sudo apt-get install lockfile-progs`.

Usage
-----

**torrential**

    Usage: torrential <allow|deny|status>

    allow               create firewall rule allowing incoming connections
    deny                remove firewall rules without prompting
    state               display state of firewall
    status              display firewall rule status

    Manipulate UFW firewall rules for BitTorrent traffic.

**torrential-wrapper**

    Usage: torrential-wrapper [ARGUMENT...]

    Wrapper around transmission-gtk to control UFW firewall rules.

License
-------

Copyright (c) 2015 Six (brbsix@gmail.com).

Licensed under the GPLv3 license.
