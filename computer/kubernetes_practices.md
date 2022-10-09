[Back](.)  

# 学习准备

* 官方文档：[https://kubernetes.io/docs/home/](https://kubernetes.io/docs/home/)

* 模拟生产环境：[Create a Kubernetes Cluster using Virtualbox — The Hard Way](https://medium.com/@mojabi.rafi/create-a-kubernetes-cluster-using-virtualbox-and-without-vagrant-90a14d791617)
* 国内的模拟生产环境：https://blog.csdn.net/qq_24872115/article/details/106280027

## 需要安装一个代理

用Virtualbox安装类生产环境的时候，由于需要访问到Google，所以需要安装一个代理，我用的[Clash](https://mxy493.xyz/2020101017609/)。这是Web代理，在终端是无法使用的，所以需要单独配置代理。

比如：vim ~/.zshrc

```
alias proxy-on='export http_proxy=192.168.0.100:7890;export https_proxy=$http_proxy'
alias proxy-off='unset http_proxy;unset https_proxy' 
```

其中192.168.0.100是我安装Clash的机器。

执行：source ~/.zshrc

1. 开启命令: proxy-on
2. 关闭命令: proxy-off

现在可以在终端使用代理，注意只在当前标签页生效，重新打开终端或新标签页需要重新执行source ~/.zshrc和 proxy-on。

## Add the kubernetes repository

```
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
```

这一步，要指定国内的源，比如阿里源，否则可能一直连不上。

```
sudo apt-add-repository "deb http://mirrors.ustc.edu.cn/kubernetes/apt kubernetes-xenial main"
或者稍后修改：vi /etc/apt/sources.list
添加国内源：deb http://mirrors.ustc.edu.cn/kubernetes/apt kubernetes-xenial main
更新源：sudo apt-get update
```

## Initializing Kubernetes Master Node

这一步依然要指定国内愿，否则也是可能一直连不上。

```
sudo kubeadm init --apiserver-advertise-address 192.168.60.11 --control-plane-endpoint 192.168.60.11 --image-repository registry.aliyuncs.com/google_containers --kubernetes-version=v1.22.10
```

安装完毕，记录命令如下，其他节点加入集群使用：

```
kubeadm join 192.168.60.11:6443 --token wv4oy0.6grdxanb3js21bgt --discovery-token-ca-cert-hash sha256:8b5967f3eed7ddbfc819032034f9f4a1a0ac59d994e2953dbef859e1d0e0104a
```

如果这个命令遗失，可以重新生成：

```
kubeadm token create --print-join-command --v=5
```

