frequently tcpdump commands
===========================

1. Filter by host/port/protocol

    parameters:

    * `-n`: Don't convert addresses (i.e., host addresses, port numbers, etc.) to names
    * `-X`: in addition to printing the headers of each packet, print the data of each packet in hex and ASCII

    ```shell
    # filter by host
    $ tcpdump -i eth1 -n -X src host 10.19.66.62

    # filter by port
    $ tcpdump -i eth1 -n -X src host 10.19.66.62 and dst port 80

    # filter by protocol
    $ tcpdump -i eth1 -n -X src host 10.19.66.62 and dst port 80 and tcp

    # capture all HTTP GET requests
    $ tcpdump -i eth1 -n -A src host 10.19.66.62 and dst port 80 and tcp[20:4]=0x47455420
    ```

    Reference [tcpdump：理论、自动抓包及业务架构树的生成](http://www.yunweipai.com/archives/7981.html).

# Reference

1. [tcpdump：理论、自动抓包及业务架构树的生成](http://www.yunweipai.com/archives/7981.html)
