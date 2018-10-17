## kubectl命令概览
![avatar](../images/kubectl-command.jpg)

## 部分重要命令参数详情
参数		|命令	|可选项
----	|----	|----
create	|clusterrole<br>clusterrolebinding<br>configmap<br>deployment<br>job<br>namespace<br>poddisruptionbudget<br>priorityclass<br>quota<br>role<br>rolebinding<br>secret<br>service<br>serviceaccount|--allow-missing-template-keys=true<br>--dry-run=false<br>--edit=false<br>-f, --filename=[]<br>-o, --output=''<br>--raw=''<br>--record=false<br>-R, --recursive=false<br>--save-config=false<br>-l, --selector=''<br>--template=''<br>--validate=true<br>--windows-line-endings=false
get		|all<br>certificatesigningrequests (aka 'csr')<br>clusterrolebindings<br>clusterroles<br>clusters (valid only for federation apiservers)<br>componentstatuses (aka 'cs')<br>configmaps (aka 'cm')<br>controllerrevisions<br>cronjobs<br>daemonsets (aka 'ds')<br>deployments (aka 'deploy')<br>endpoints (aka 'ep')<br>events (aka 'ev')<br>horizontalpodautoscalers (aka 'hpa')<br>ingresses (aka 'ing')<br>jobs<br>limitranges (aka 'limits')<br>namespaces (aka 'ns')<br>networkpolicies (aka 'netpol')<br>nodes (aka 'no')<br>persistentvolumeclaims (aka 'pvc')<br>persistentvolumes (aka 'pv')<br>poddisruptionbudgets (aka 'pdb')<br>podpreset<br>pods (aka 'po')<br>podsecuritypolicies (aka 'psp')<br>podtemplates<br>replicasets (aka 'rs')<br>replicationcontrollers (aka 'rc')<br>resourcequotas (aka 'quota')<br>rolebindings<br>roles<br>secrets<br>serviceaccounts (aka 'sa')<br>services (aka 'svc')<br>statefulsets<br>storageclasses<br>thirdpartyresources|--all-namespaces=false<br>--allow-missing-template-keys=true<br>--chunk-size=500<br>--export=false<br>--field-selector=''<br>-f, --filename=[]<br>--ignore-not-found=false<br>--include-uninitialized=false<br>-L, --label-columns=[]<br>--no-headers=false<br>-o, --output=''<br>--raw=''<br>-R, --recursive=false<br>-l, --selector=''<br>--server-print=true<br>--show-kind=false<br>--show-labels=false<br>--sort-by='' <br>--template=''<br>--use-openapi-print-columns=false<br>-w, --watch=false<br>--watch-only=false
run		|NAME	|--allow-missing-template-keys=true<br>--attach=false<br>--cascade=true<br>--command=false<br>--dry-run=false<br>--env=[]<br>--expose=false<br>-f, --filename=[]<br>--force=false<br>--generator=''<br>--grace-period=-1<br>--hostport=-1<br>--image=''<br>--image-pull-policy=''<br>-l, --labels=''<br>--leave-stdin-open=false<br>--limits=''<br>-o, --output=''<br>--overrides=''<br>--pod-running-timeout=1m0s<br>--port=''<br>--quiet=false<br>--record=false<br>-R, --recursive=false<br>-r, --replicas=1<br>--requests=''<br>--restart='Always'<br>--rm=false<br>--save-config=false<br>--schedule=''<br>--service-generator='service/v2'<br>--service-overrides=''<br>--serviceaccount=''<br>-i, --stdin=false<br>--template=''<br>--timeout=0s<br>-t, --tty=false<br>--wait=false	

## 部分使用示例
1.创建资源
```
kubectl create -f my-service.yaml -f my-rc.yaml
```

2.查看资源
```
kubectl get rc,svc,pods -o wide --all-namespaces
```

3.查看node/pod信息
```
kubectl describe nodes/pods [node-name]/[pod-name]
```

4.修改资源（比如修改副本数量，增加、修改label，更改image版本，修改端口等）
```
kubectl replace/apply -f my-rc.yaml
kubectl scale rc rc-name --replicas=3
```

5.删除pod
```
kubectl delete -f pod.yaml
kubectl delete pods --all
```

6.通过bash获得Pod中某个容器的TTY
```
kubectl exec -it [pod-name] -c [container-name] /bin/bash
```

7.编辑资源文件
```
kubectl edit service/rc/pod [svc name]/[rc name]/[pod name]
```

8.下线node（会将此node设置为不可用，并迁移其中的pod）
```
kubectl drain node ip或name
```