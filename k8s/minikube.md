# Minikube

- [安裝與啟動教學](https://minikube.sigs.k8s.io/docs/start/)

- [Push images](https://minikube.sigs.k8s.io/docs/handbook/pushing/)


綁定當前 terminal docker 為 minicube cluster 的 docker
```
eval $(minikube docker-env)
```

後續 docker build 的 image 就會建構在 minikube 中，記得在 yaml 檔案裡標記 `imagePullPolicy: IfNotPresent` minikube 才會先查找 local image