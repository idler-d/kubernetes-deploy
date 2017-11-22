centos7 & kubernetes & flannel & kubeadm

使用kubeadm安装kubernetes容器化组件安装flannel的overlay网络。
这个网咯下部署的service会被宿主机的容器内核的iptables拦截。

这时候需要手工添加iptables规则。

```
iptables -I INPUT -s xxx.xxx.xxx.0/24 -j ACCEPT
iptables -I FORWARD -j ACCEPT
```
    
内核iptables重启会重置原规则。所以把规则放进开机启动脚本中。

```
chmod +x /etc/rc.d/rc.local
echo 'iptables -I INPUT -s xxx.xxx.xxx.0/24 -j ACCEPT' >> /etc/rc.d/rc.local
echo 'iptables -I FORWARD -j ACCEPT' >> /etc/rc.d/rc.local
```