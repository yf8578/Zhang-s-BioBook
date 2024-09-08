---
description: 为jupyter lab配置指定版本python，R内核
---

# 基于conda构建个性化分析镜像

目前我理解的云平台上镜像主要有<mark style="color:orange;">**两种类型**</mark>，一种是只能用于来构建分析流程的，另一种是能够进行个性化分析（支持jupyter lab，能够选择不同内核），且也能够用来构建分析流程。

这里主要还是介绍如何<mark style="color:orange;">**基于含有conda的预设镜像**</mark>构建用于个性化分析流程的镜像。

## 新建镜像

在镜像管理中选择<mark style="color:orange;">**新建镜像**</mark>

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

镜像来源有两种类型可以选择，这里选择<mark style="color:orange;">**含有conda的预设镜像stereonote**</mark>

<mark style="color:red;">**注意：通过外源导入的镜像可用于项目>流程分析>工作流模块构建WDL，暂不支持用于项目>数据分析 (Stereonote) 模块。**</mark>

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

选择之后如果有什么需要用到的python或R包，可以将包的名称填在“工具包级版本”中，这部分可以参照官方手册。需要注意的是，深圳片区如果要构建sudo权限的镜像需在Bash指令中添加以下命令。

```sh
mkdir /etc/yum.repos.d/bak
mv /etc/yum.repos.d/*.repo /etc/yum.repos.d/bak
wget -O /etc/yum.repos.d/Centos-7.repo http://mirrors1.sz.cngb.org/repository/os/repo/Centos-7.repo
wget -O /etc/yum.repos.d/epel.repo http://mirrors1.sz.cngb.org/repository/os/repo/epel7.repo
yum clean all
yum makecache
yum install -y sudo

chmod 444 /etc/sudoers
echo -e "stereonote\tALL=(ALL)\tNOPASSWD: ALL" >> /etc/sudoers
```

待状态变为“构建成功”，即可打开个性分析，同样选择新建分析，选择合适的资源配置xxxx，<mark style="color:orange;">**选择刚才构建的镜像，运行即可。**</mark>

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

## 个性化配置环境

### jupyter lab添加R内核

可以简单运行一些命令测试一下，现在是具有sudo权限的。

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

同时也可以看到这个R的版本着实有些低了，下面我们借助conda来安装一个4.4.1版本的R，并将其配置到jupyter lab的内核中。

```sh
source /opt/conda/bin/activate
conda create -n r441
conda activate r441
conda install conda-forge::r-base
```

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

安装好R之后，需要进一步安装内核进行配置。

```sh
conda install conda-forge::r-irkernel
```

安装完 `r-irkernel` 后，将这个环境中的 R kernel 安装到 `base` 环境中的 Jupyter 中：

<pre class="language-sh"><code class="lang-sh"><strong>R -e "IRkernel::installspec(name = 'ir441', displayname = 'R 4.4.1 (r441)')"
</strong></code></pre>

* `name = 'ir441'`：给这个 kernel 起一个名称（`ir441`），方便区分。
* `displayname = 'R 4.4.1 (r441)'`：Jupyter 中显示的名称。

大功告成

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### jupyter lab添加python内核

和之前操作差不多，创建一个新的虚拟环境，安装指定版本的python，内核，进行配置即可，可以参照下面的代码。

```
conda create -n py311
conda activate py311
conda install python=3.11
conda install ipykernel
python -m ipykernel install --user --name py311 --display-name "Python 3.11 (py311)"
```

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<mark style="color:red;">**注意注意注意！！！！！**</mark>

<mark style="color:red;">**退出前保存当前环境为一个新的镜像，要不然前功尽弃ε=(´ο｀\*)))唉**</mark>
