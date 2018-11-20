# k8s单机部署

---

## 关闭centos防火墙
```
systemctl disable firewalld
systemctl stop firewalld
```

## 安装etcd和k8s（会自动安装docker）
```
yum install -y etcd kubernetes
```

## 修改配置
```
1、vi /etc/sysconfig/docker
2、OPTIONS='--selinux-enabled=false --insecure-registry gcr.io'

1、$ vi /etc/kubernetes/apiserver
2、找到这一行 "KUBE_ADMISSION_CONTROL="--admission_control=NamespaceLifecycle,NamespaceExists,LimitRanger,SecurityContextDeny,ServiceAccount,ResourceQuota"，去掉ServiceAccount，保存退出。

1、yum install *rhsm*
2、wget http://mirror.centos.org/centos/7/os/x86_64/Packages/python-rhsm-certificates-1.19.10-1.el7_4.x86_64.rpm
3、rpm2cpio python-rhsm-certificates-1.19.10-1.el7_4.x86_64.rpm | cpio -iv --to-stdout ./etc/rhsm/ca/redhat-uep.pem | tee /etc/rhsm/ca/redhat-uep.pem
4、docker pull registry.access.redhat.com/rhel7/pod-infrastructure:latest
```

## 启动服务
```
systemctl start etcd
systemctl start docker
systemctl start kube-apiserver
systemctl start kube-controller-manager
systemctl start kube-scheduler
systemctl start kubelet
systemctl start kube-proxy
```

## 启动mysql
```
kubectl create -f mysql-rc.yaml
kubectl get rc
kubectl get pods
docker ps | grep mysql
kubectl create -f mysql-svc.yaml
kubectl get svc
```

## 启动tomcat
```
kubectl create -f myweb-rc.yaml
kubectl get pods
kubectl create -f myweb-svc.yaml
kubectl get services
```

## 访问页面
```
http://ip:30001/demo/
```







