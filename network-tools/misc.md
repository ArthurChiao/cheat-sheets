misc
=========

1. configure TCP keepalive

    ```shell
    $ sysctl -a | grep tcp_keepalive_

    $ sysctl -w \
        net.ipv4.tcp_keepalive_time=1800 \
        net.ipv4.tcp_keepalive_intvl=10 \
        net.ipv4.tcp_keepalive_probes=2
    ```

    Reference: [TCP-Keepalive-HOWTO](http://www.tldp.org/HOWTO/html_single/TCP-Keepalive-HOWTO/)
