Solve this question on: ssh cka3962

 

You're asked to confirm that kube-proxy is running correctly. For this perform the following in Namespace project-hamster:

1. Create Pod p2-pod with image nginx:1-alpine

2. Create Service p2-service which exposes the Pod internally in the cluster on port 3000->80

3. Write the iptables rules of node cka3962 belonging the created Service p2-service into file /opt/course/p2/iptables.txt

4.  Delete the Service and confirm that the iptables rules are gone again


```
➜ ssh cka3962


# 第一题
➜ candidate@cka3962:~$ k -n project-hamster run p2-pod --image=nginx:1-alpine
pod/p2-pod created


# 第二题
➜ candidate@cka3962:~$ k -n project-hamster expose pod p2-pod --name p2-service --port 3000 --target-port 80

➜ candidate@cka3962:~$ k -n project-hamster get pod,svc
NAME                 READY   STATUS    RESTARTS   AGE
pod/p2-pod           1/1     Running   0          2m31s

NAME                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
service/p2-service   ClusterIP   10.105.128.247   <none>        3000/TCP   1s


```



 