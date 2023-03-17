# eCue

eCue is a tool that uses CUE to test for structured data semantic equality.

These 2 YaML files are semantically equal, but not byte-for-byte equal:

- 1.yml:
```yaml
foo: 1
bar: 2
```
- 2.yml:
```yaml
bar: 2
foo: 1
```

eCue(.sh) uses CUE to check that 2 files contain the same information, even if the data is stated in a different order:

```shell
$ ./eCue.sh 1.yml 2.yml
$ echo $?
0
```

If another file is introduced, containing different structured data, and is compared to either of the first 2 files, eCue provides a CUE error message showing one more differences encountered.

```shell
$ cat 3.yml
notFoo: 1
bar: 2
$ ./eCue.sh 1.yml 3.yml 
notFoo: field not allowed:
    ./3.yml:1:2
    ../../../../tmp/tmp.RWnZAU5cQN.cue:1:10
$ echo $?
1
```
