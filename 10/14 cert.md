

Perform some tasks on cluster certificates:

1. Check how long the kube-apiserver server certificate is valid using openssl or cfssl. Write the expiration date into /opt/course/14/expiration. Run the kubeadm command to list the expiration dates and confirm both methods show the same one
> 使用openssl或cfssl检查kube- apisserver服务器证书的有效期。将截止日期写入/opt/course/14/expiration。运行kubeadm命令列出过期日期，并确认这两种方法显示的是相同的

2. Write the kubeadm command that would renew the kube-apiserver certificate into /opt/course/14/kubeadm-renew-certs.sh
> 将更新kube- apisserver证书的kubeadm命令写入/opt/course/14/kubeadm-renew-cert .sh



Answer:
First let's find that certificate:

// 默认的证书路径

```
➜ ssh cka9412

➜ candidate@cka9412:~$ sudo -i

➜ root@cka9412:~# find /etc/kubernetes/pki | grep apiserver
/etc/kubernetes/pki/apiserver-etcd-client.key
/etc/kubernetes/pki/apiserver-kubelet-client.key
/etc/kubernetes/pki/apiserver-etcd-client.crt
/etc/kubernetes/pki/apiserver.key
/etc/kubernetes/pki/apiserver-kubelet-client.crt
/etc/kubernetes/pki/apiserver.crt
```


<!-- 知识点- 解析证书的命令 -->

```

➜ root@cka9412:~# openssl x509 -noout -text -in /etc/kubernetes/pki/apiserver.crt | grep Validity -A2
        Validity
            Not Before: Oct 29 14:14:27 2024 GMT
            Not After : Oct 29 14:19:27 2025 GMT

```
// kubeadm 获取证书过期时间

```
➜ root@cka9412:~# kubeadm certs check-expiration | grep apiserver
apiserver                  Oct 29, 2025 14:19 UTC   356d    ca         no      
apiserver-etcd-client      Oct 29, 2025 14:19 UTC   356d    etcd-ca    no      
apiserver-kubelet-client   Oct 29, 2025 14:19 UTC   356d    ca         no 
```

> 证书续签的 kubeadm 命令

```
➜ root@cka9412:~# kubeadm alpha certs renew all
```



