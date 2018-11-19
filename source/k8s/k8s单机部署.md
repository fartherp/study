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
OPTIONS='--selinux-enabled=false --insecure-registry gcr.io'
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







