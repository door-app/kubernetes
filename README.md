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