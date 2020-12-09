# Konstantinov86_platform
Konstantinov86 Platform repository

Выполнено ДЗ № 1

 - [V] Основное ДЗ
 - [V] Задание со *

## В процессе сделано:
 - Выполнена установка   minikube:
` kubernetesintro git:(kubernetes-intro) kubectl cluster-info
Kubernetes master is running at https://192.168.64.2:8443
KubeDNS is running at https://192.168.64.2:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy`;
- Ознакомлен с интерфейсом dashboard;
- Разберитесь почему все pod в namespace kube-system восстановились после удаления:
kube-proxy -  управляется daemonset;
core-dns -  управляется deployment;
kube-apiserver- static pod -управляется kubelet;
-  создан  dockerfile согласно требованиям,образ собран и залит в dockerhub;
- Написан манифест web-pod.yaml;
- Выясните причину, по которой pod frontend находится в статусе Error:
`panic: environment variable "PRODUCT_CATALOG_SERVICE_ADDR" not set`;
Соответственно данная переменная присутствует в   frontend-pod.yaml.
## Как запустить проект:
- docker build -t wenger23/nginx:3.0 . & docker run wenger23/nginx:3.0 -d -p 8000:8000;
- kubectl apply -f web-pod.yaml;
- kubectl apply frontend-pod-healthy.yaml;

## Как проверить работоспособность:
-  перейти по ссылке http://localhost:8000/homework.html;
- kubectl port-forward --address 0.0.0.0 pod/web 8000:8000;


## PR checklist:
 - [V] Выставлен label с темой домашнего задания
