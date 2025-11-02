

Preview Question 3 | Change Service CIDR
Solve this question on: ssh cka9412

1.Create a Pod named check-ip in Namespace default using image httpd:2-alpine

2. Expose it on port 80 as a ClusterIP Service named check-ip-service. Remember/output the IP of that Service

3. Change the Service CIDR to 11.96.0.0/12 for the cluster

4. Create a second Service named check-ip-service2 pointing to the same Pod

ℹ️ The second Service should get an IP address from the new CIDR range



```bash

➜ candidate@cka9412:~$ k run check-ip --image=httpd:2-alpine
pod/check-ip created

➜ candidate@cka9412:~$ k expose pod check-ip --name check-ip-service --port 80



➜ candidate@cka9412:~$ k get svc
NAME              TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
check-ip-service   ClusterIP   10.96.114.108   <none>        80/TCP    10s
kubernetes         ClusterIP   10.96.0.1       <none>        443/TCP   2d23h


```


```bash

➜ candidate@cka9412:~$ sudo -i

➜ root@cka9412:~# vim /etc/kubernetes/manifests/kube-apiserver.yaml


```