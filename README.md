# KubeMast

### Kubernetes Metrics Server 安装说明
项目地址：https://github.com/kubernetes-incubator/metrics-server
主要使用https://github.com/kubernetes-incubator/metrics-server/tree/master/deploy/1.8%2B这个这些文件，想办法弄下来。

### 修改相关文件
1. 在metrics-server-deployment.yaml中新增如下配置
```
command:
- /metrics-server
- --kubelet-preferred-address-types=InternalIP
- --kubelet-insecure-tls
- --metric-resolution=30s
```
2. 修改镜像地址
k8s.gcr.io/metrics-server-amd64:v0.3.3替换为registry.cn-hangzhou.aliyuncs.com/google_containers/metrics-server-amd64:v0.3.3
3. 最终文件见本项目metrics_server文件下metrics-server-deployment.yaml文件
4. 部署Metrics Server
```shell
kubectl apply -f metrics_server/
```
5. 检查部署是否成功,出现如下结果说明部署成功
```
[root@node01 metrics]# kubectl top node
NAME     CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%   
node01   202m         10%    2234Mi          60%       
node02   628m         31%    1423Mi          38%       
node03   149m         7%     1278Mi          34% 
```