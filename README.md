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

  <details><summary>ДЗ № 4</summary>

 - [V] Основное ДЗ
 - [V] Задание со *

## В процессе сделано:
- [V] Добавил пробы в под;
- [V] Создал deployment со стратегией обновления;
- [V] Создал service и включил ipvs;
- [V] Установил Metalb и настроил маршрутизацию;
- [V] открыл доступ к coreDNS;
- [V] установил и открыл доступ к dashboard;
## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>

  <details><summary>ДЗ № 5</summary>

 - [V] Основное ДЗ
 - [V] Задание со *

## В процессе сделано:
- [V] Создал statefulset minio;
- [V] Создал headless service;
- [V] Gроверил работу minio;
- [V] Сделал statefulset c secret
## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>

 <details><summary>ДЗ № 6</summary>

 - [V] Основное ДЗ
 - [V] Задание со *

## В процессе сделано:
- [V] Создан кластер в Google Cloud;
- [V] Установлен из Helm - ingress-nginx и cert-manager;
- [V] Создан issuer lets encrypt для certmanager;
- [V] Установлен и кастомизирован chartmuseum -https://chartmuseum.35.228.182.231.nip.io/;
- [V] * Работа с chartmuseum:
Активируем api в values.yaml - DISABLE_API: false;
Создадим собственный чарт - helm create mychart;
Запакуем - helm package .;
Запушим в репозиторий - curl --data-binary "@mychart-0.1.0.tgz" https://chartmuseum.35.228.182.231.nip.io/api/chart;
Обновим - helm repo update ;
Установим - helm install mychart chartmuseum/mychart;
- [V] Установлен harbor - https://harbor.35.228.182.231.nip.io/;
- [V] * Описана установка nginx-ingress, cert-manager и harbor в helmfile;
- [V] Создан свой helmchart  hipster-shop;
- [V] * Добавлен requirements.yaml (dependencies.yaml в helm 3) redis;
- [V] Создан деплой при помощи kubecfg;
- [V] Создан деплой при помощи kustomize(test и prod).

## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>

 <details><summary>ДЗ № 7</summary>

 - [V] Основное ДЗ
 - [V] Задание со *

## В процессе сделано:
- [V] Создан CustomResource и CustomResourceDefinition my-sql;
- [V] Сделана Валидация;
- [V] Создан контроллер ;
- [V] Собран образ контроллера -залит на dockerhub - wenger23/otus_demo:0.1 ;
- [V] проверка работоспособности контроллера :
major@MacBook-Air  ~/virtual/Konstantinov86_platform/kubernetes-operator/deploy   kubernetes-operator  
kubectl get jobs
NAME                         COMPLETIONS   DURATION   AGE
backup-mysql-instance-job    1/1           3s         2m18s
restore-mysql-instance-job   1/1           45s        82s

major@MacBook-Air  ~/virtual/Konstantinov86_platform/kubernetes-operator/deploy   kubernetes-operator  kubectl exec -it $MYSQLPOD -- mysql -potuspassword -e "select * from test;" otus-database
mysql: [Warning] Using a password on the command line interface can be insecure.
+----+-------------+
| id | name        |
+----+-------------+
|  1 | some data   |
|  2 | some data-2 |
|  3 | some data-2 |
|  4 | some data-2 |
|  5 | some data-2 |
+----+-------------+
## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>

 <details><summary>ДЗ № 8</summary>

 - [V] Основное ДЗ
 - [V] Задание со *

## В процессе сделано:
- [V] Создан кастомный деплоймент и сервис nginx  -deployment.yaml,service.yaml;
- [V] Выбран 2й вариант сложности - Поставить prometheus-operator через kubectl apply из офф.
репозитория (Bring`em on!)
- [V] Создан деплоймент и сервис nginx exporter;
- [V] Создан serivcemonitor.yaml ,который смотрит на nginx exporter;
- [V] Работа выполнялась в google cloud - сделаны ингресс сервисы /ingress-services/ingress-grafana.yaml ingress-prometheus.yaml для проброса наружу grafana и prometheus:

https://prometheus.35.228.182.231.nip.io/targets
https://grafana.35.228.182.231.nip.io/ - admin/admin - dashboard - NGINX exporter
## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>

 <details><summary>ДЗ № 6</summary>

 - [V] Основное ДЗ
 - [V] Задание со *