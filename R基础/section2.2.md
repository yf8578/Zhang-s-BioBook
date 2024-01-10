# Section 2.2
## 小技巧
### 转移R包
```R
oldip <- installed.packages()[,1]
save(oldip, file = "installedPacckages.Rdata")
#在B设备/版本上进行安装；
load("installedPacckages.Rdata")
newip <- installed.packages()[,1]
for (i in setdiff(oldip,newip)) {  install.packages(i)}
```
