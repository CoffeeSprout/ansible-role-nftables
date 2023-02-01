coffeesprout.nftables
=========

Setup and maintain nftables for your servers.
This role doesn't aim to be the most complete or flexible, just set some rules for in / out traffic, nat.
If there is something that isn't cover you can provide your own templates.

Requirements
------------

A modern Linux disto with NFTables support

Role Variables
--------------

For a full list, have a look at the defaults/main.yml.
These are the most interesting

Enable loading NAT rules; Default False
        
        nft_enable_gateway: False


In case of NAT this specifies the "outgoing" network connection through wich the traffic leaves the local network

        nft_ext_if: "{{ ansible_default_ipv4.interface }}"

In case of NAT; This is the from address used in SNAT

        nft_ip_pub: "{{ ansible_default_ipv4.address }}"

Default drop all inbound traffic except when allowed with nft_tcp_pass_in or nft_udp_pass_in

        nft_inbound_policy: drop

Default drop all outbound traffic except when allowed with nft_tcp_pass_out or nft_udp_pass_out

        nft_outbound_policy: accept

Specify inbound TCP traffic allowed

        nft_tcp_pass_in:
        - "{{ sshd_port | default('22') }}"

Specify outbound TCP traffic allowed

        nft_tcp_pass_out:
        - 22
        - 80
        - 443

Specify inbound UDP traffic allowed

        nft_udp_pass_in:
        - 53
        - 123
        - 443

Specify outbound UDP traffic allowed

        nft_udp_pass_out:
        - 53
        - 123
        - 443


Example Playbook
----------------

Simple setup that allows SSH in, SSH/HTTP/HTTPS and DNS

    - hosts: servers
      roles:
      - role: coffeesprout.nftables


License
-------

BSD

Author Information
------------------

Just reach out on Github
