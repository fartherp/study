# 解决kubectl get pods时 No resources found.问题

---

```
1、$ vi /etc/kubernetes/apiserver
2、找到这一行 "KUBE_ADMISSION_CONTROL="--admission_control=NamespaceLifecycle,NamespaceExists,LimitRanger,SecurityContextDeny,ServiceAccount,ResourceQuota"，去掉ServiceAccount，保存退出。
3、systemctl restart kube-apiserver  重启此服务
```




