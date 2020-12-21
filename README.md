# Konstantinov86_platform
Konstantinov86 Platform repository


<details><summary>ДЗ № 1</summary>

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
 </details>

 <details><summary>ДЗ № 2</summary>

 - [V] Основное ДЗ
 - [V] Задание со *

## В процессе сделано:
 - создание replicaset frontend-replicaset.yaml:
 - Добавление label selection для корректной работы;
 - создание deployment paymentservice-replicaset.yaml;
- создание deployment strategy blue-green и reverse;
- создание daemonset node-exporter-daemonset.yaml;
- создание daemonset node-exporter-daemonset.yaml с запуском на мастер ноде :
`tolerations:
        - key: node-role.kubernetes.io/master
          effect: NoSchedule`
## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>

 <details><summary>ДЗ № 3</summary>

 - [V] Основное ДЗ

## В процессе сделано:
- [V] Создал Service Account bob, дать ему роль admin в рамках всего
кластера;
- [V] Создал Service Account dave без доступа к кластеру
- [V] Создал Namespace prometheus;
- [V] Создал Service Account carol в этом Namespace;
- [V] Дал всем Service Account в Namespace prometheus возможность
делать get, list, watch в отношении Pods всего кластера;
- [V] Создал Namespace dev;
- [V] Создал Service Account jane в Namespace dev;
- [V] Дал jane роль admin в рамках Namespace dev;
- [V] Создал Service Account ken в Namespace dev;
- [V] Дал ken роль view в рамках Namespace dev.

## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>
