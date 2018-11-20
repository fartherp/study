# Kubernetes创建pod一直处于ContainerCreating排查和解决

---

## 解决方案
```
1、yum install *rhsm*
2、wget http://mirror.centos.org/centos/7/os/x86_64/Packages/python-rhsm-certificates-1.19.10-1.el7_4.x86_64.rpm
3、rpm2cpio python-rhsm-certificates-1.19.10-1.el7_4.x86_64.rpm | cpio -iv --to-stdout ./etc/rhsm/ca/redhat-uep.pem | tee /etc/rhsm/ca/redhat-uep.pem
4、docker pull registry.access.redhat.com/rhel7/pod-infrastructure:latest
```




