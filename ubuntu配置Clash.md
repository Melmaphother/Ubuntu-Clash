## 该文档是我在使用Ubuntu虚拟机配置Clash时的一些记录

### 硬件平台

- PC平台：Windows 11
- 虚拟机平台：VMWare Workstation Pro
- Linux发行版：Ubuntu-22.04.1

### 为什么要配置Clash

虚拟机不与主体机共享网络？（~~没有学过网络相关的知识，所以不太了解其中的详细原理~~）但是显然在Ubuntu Network设置中有设置网络代理（Network Proxy）这一选项，也就意味着：

- 当我们在虚拟机中使用网络时，如果仅仅使用大陆允许的网络链接，自然可以把Network Proxy中的选项改为Automatic。

- 但是当我们需要访问一些诸如[Github](https://github.com)，[youtube](https://youtube.com)等等网站需要解决开发中的问题的时候，上述方法就不可行了，在Windows上我们自然可以选择使用网络代理平台[Clash](https://github.com/Fndroid/clash_for_windows_pkg/releases)，通过订阅链接进行下载，