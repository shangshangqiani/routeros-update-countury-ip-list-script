# routeros-update-countury-ip-list-script
routeros更新国家ip列表脚本
## 以中国```CN```为例:
### 删除旧CNfile
```yaml
:if [/file find name=CN] do={/file remove [find name=CN]; :log info ("The file cleanup successful")} else={/tool fetch url=http://www.iwik.org/ipcountry/mikrotik/CN}
```
### 下载新CNfile
```yaml
:if [/file find name=CN] do={:log info ("The file download successful")} else={/tool fetch url=http://www.iwik.org/ipcountry/mikrotik/CN; :log info ("The file download successful")}
```
### (与下面的Force_CNlist对应否则脚本失效)
未被阻断的一些域名，例如:[speedtest.net](www.speedtest.net)
```yaml
/ip firewall address-list
disable [find address=example.com]
```
### 删除旧CNlist
```yaml
:if [/ip firewall address-list find list=CN] do={/ip firewall address-list remove [find list=CN]; :log info ("The list cleanup successful")} else={/import file-name=CN}
```
### 导入新CNlist
```yaml
:if [/ip firewall address-list find list=CN] do={:log info ("The list import successful")} else={/import file-name=CN; :log info ("The list import successful")}
```
### Force_CNlist
```yaml
/ip firewall address-list
add address=example.com list=CN
```
## 合并
```yaml
#删除旧CNfile
:if [/file find name=CN] do={/file remove [find name=CN]; :log info ("The file cleanup successful")} else={/tool fetch url=http://www.iwik.org/ipcountry/mikrotik/CN}
#下载新CNfile
:if [/file find name=CN] do={:log info ("The file download successful")} else={/tool fetch url=http://www.iwik.org/ipcountry/mikrotik/CN; :log info ("The file download successful")}
#(与下面的Force_CNlist对应否则脚本失效)
/ip firewall address-list
disable [find address=example.com]
#删除旧CNlist
:if [/ip firewall address-list find list=CN] do={/ip firewall address-list remove [find list=CN]; :log info ("The list cleanup successful")} else={/import file-name=CN}
#导入新CNlist
:if [/ip firewall address-list find list=CN] do={:log info ("The list import successful")} else={/import file-name=CN; :log info ("The list import successful")}
#Force_CNlist
/ip firewall address-list
add address=example.com list=CN
```
