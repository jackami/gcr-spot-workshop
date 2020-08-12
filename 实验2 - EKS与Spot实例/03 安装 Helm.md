# 安装 Helm

执行如下安装命令. 
(注意不要执行 'helm init'. 如果不小心执行, 可以通过执行 'helm reset –force' 进行restore.)

```
cd ~/environment
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh
chmod +x get_helm.sh
./get_helm.sh
```

执行如下配置命令为 tiller 创建 service account 配置文件

```
cat <<EoF > ~/environment/rbac.yaml
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tiller
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: tiller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: tiller
    namespace: kube-system
EoF
```

执行如下配置命令为 tiller 创建 service account

```
kubectl apply -f ~/environment/rbac.yaml
```

安装 tiller 命令如下. 安装成功系统会显示 "...Tiller (the Helm server-side component) has been installed into your Kubernetes Cluster..."

```
helm init --service-account tiller
```
