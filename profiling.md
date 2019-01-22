查看调用树

```shell
$ perf record -a --call-graph -p some_pid

$ perf report --call-graph --stdio -G
```
