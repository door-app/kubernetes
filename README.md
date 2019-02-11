## local
### minikubeのbuilt-in Docker daemonを使用するように設定
↓ターミナル別でやらないとダメ
```
eval $(minikube docker-env)
eval "$(docker-machine env -u)"
```
※latestは使えない

### minikube ingress
```
$ minikube addons enable ingress
$ minikube addons list
```

### hostsに登録
```
echo "$(minikube ip) door.local
```

### CURL
```
curl -I http://`minikube ip` -H 'Host: door.local'
curl http://`minikube ip` -H 'Host: door.local'
```

## istio
```
$ helm template istio-1.0.5/install/kubernetes/helm/istio --name istio --namespace istio-system --set grafana.enable=true --set security.enabled=true > istio.yaml
--set security.enable=true を入れないとPod(istio-security-post-install)がCrashLoopBackOffになる
```
```
ネームスペース作成
$ kubectl create namespace istio-system
istio.yamlを適用
$ kubectl apply -f istio.yaml
```

##CURL
```
port
$ kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}'
ip 
$ minikube ip
$ curl http://`minikube ip`:31380 -H 'Host: door.local'
```




