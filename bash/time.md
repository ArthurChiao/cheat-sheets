time utils
==============

1. date

    ```shell
    $ date +%Y%m%d%H%M%S
    20160623152444 

    $ date +%Y-%m-%d::%H:%M:%S
    2016-06-23::15:26:06

    # generate file name
    $ echo "file-`date +%Y%m%d%H%M%S`.txt"
    file-20160623153601.txt 
    ```
