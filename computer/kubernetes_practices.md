[Back](.)  

# 学习准备

* 官方文档：[https://kubernetes.io/docs/home/](https://kubernetes.io/docs/home/)

* 模拟生产环境：[Create a Kubernetes Cluster using Virtualbox — The Hard Way](https://medium.com/@mojabi.rafi/create-a-kubernetes-cluster-using-virtualbox-and-without-vagrant-90a14d791617)
* 国内的模拟生产环境：https://blog.csdn.net/qq_24872115/article/details/106280027

用Virtualbox安装类生产环境的时候，由于需要访问到Google，所以需要安装一个代理，我用的Clash。这是Web代理，在终端是无法使用的，所以需要单独配置代理。

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