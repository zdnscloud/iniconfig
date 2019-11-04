# 说明
该软件包实现了一种ini配置文件解析器语言

配置文件由多个部分组成，以“ [section] ”标题开头，后跟“ name value ”条目

> 前后的空格已从值中删除

例如：
```
    [INPUT]
        Name             tail
        Path             /var/log/containers/*.log
        Parser           docker
        Tag              kube.*
        Refresh_Interval 5
        Mem_Buf_Limit    5MB
        Skip_Long_Lines  On

    [FILTER]
        Name   kubernetes
        Match  kube.*

    [OUTPUT]
        Name  es
        Match *
        Host  elasticsearch-master
        Port  9200
        Logstash_Format On
        Retry_Limit False
```
# 使用

## 读取文件
```
  cfg := iniconfig.NewDefault()
  file, err := os.Open(fname)
  cfg.Read(bufio.NewReader(file))
```
## 读取字符串
```
  cfg := iniconfig.NewDefault()
  cfg.Read(bufio.NewReader(strings.NewReader(str)))
```
  
