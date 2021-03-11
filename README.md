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

<details><summary>ДЗ № 9</summary>

 - [V] Основное ДЗ
 - [V] Задание со *

## В процессе сделано:
- [V] Создан кластер в GCP с 4 нодами (3 infra + default);
- [V] Задеплоен hipstershop;
- [V] Развернут EFK стек -сделан tls kibana.35.228.165.216.nip.io,elasticsearch запущен на выделенных нодах с толерейшенами;
- [V] Развернут ingress-nginx на выделенных нодах;
- [V] Настройка fluentbit - указан elastic master;
- [V]* Решена проблема с дублирующими полями -по статье https://bk0010-01.blogspot.com/2020/03/fluent-bit-and-kibana-in-kubernetes.html - приложен fluentbit.values.yaml;
- [V] Установлен prometheus и elastic-exporter;
- [V] Установлен fluentbit на выделенные ноды для парсинга ingress-nginx,донастроен конфиг ингресс для отдачи логов в json;
- [V] Создан дэшборд в кибане и выгружен в export.ndjson;
- [V] Установлен Loki и Promtail и модифицирован prometheus для создания loki датасурса prometheus-operator.values.yaml;
- [V] Создан dashboard в grafana  для loki


## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>

 
<details><summary>ДЗ № 10</summary>

 - [V] Основное ДЗ
 - [V] Задание со *

## В процессе сделано:
- [V] Создан проект в gitlab - https://gitlab.com/wenger23/microservices-demo;
- [V] Скопирован репозиторий hispter-shop и добавлены helmcharts - deploy/charts;
- [V] Развернут кластер в GCP с помощью terraform + установлен istio GKE;
- [V] * Автоматизировано создание кластера с помощью terraform через gitlab приложен файл - gitlab-terraform/.gitlab-ci.yml,ссылка на репозиторий - https://gitlab.com/wenger23/infra;
- [V] * Создан pipeline в gitlab : сборка всех образов(kaniko) по тэгу,с использвованием CI_COMMIT_TAG в версии образа,и пуш образов в gitlab registry ,файл gitlab-microservices/.gitlab-ci.yaml;
- [V] Установлен helmrelease,flux,fluxctl -реазилована CD стратегия - коммит с тэгом => сборка новой версии образа =>
деплой в кластер:
` major@MacBook-Air  ~  kubectl get helmrelease -n microservices-demo
NAME                    RELEASE                 PHASE       STATUS     MESSAGE                                                                                    AGE
adservice               adservice               Succeeded   deployed   Release was successful for Helm release 'adservice' in 'microservices-demo'.               47h
cartservice             cartservice             Succeeded   deployed   Release was successful for Helm release 'cartservice' in 'microservices-demo'.             10h
checkoutservice         checkoutservice         Succeeded   deployed   Release was successful for Helm release 'checkoutservice' in 'microservices-demo'.         47h
currencyservice         currencyservice         Succeeded   deployed   Release was successful for Helm release 'currencyservice' in 'microservices-demo'.         47h
emailservice            emailservice            Succeeded   deployed   Release was successful for Helm release 'emailservice' in 'microservices-demo'.            47h
frontend                frontend                Succeeded   deployed   Release was successful for Helm release 'frontend' in 'microservices-demo'.                161m
loadgenerator           loadgenerator           Succeeded   deployed   Release was successful for Helm release 'loadgenerator' in 'microservices-demo'.           78m
paymentservice          paymentservice          Succeeded   deployed   Release was successful for Helm release 'paymentservice' in 'microservices-demo'.          47h
productcatalogservice   productcatalogservice   Succeeded   deployed   Release was successful for Helm release 'productcatalogservice' in 'microservices-demo'.   47h
recommendationservice   recommendationservice   Succeeded   deployed   Release was successful for Helm release 'recommendationservice' in 'microservices-demo'.   47h
shippingservice         shippingservice         Succeeded   deployed   Release was successful for Helm release 'shippingservice' in 'microservices-demo'.         47h`
- [V] лог изменения frontend в чарте:
`ts=2021-03-08T15:58:43.246859639Z caller=release.go:79 component=release release=frontend targetNamespace=microservices-demo resource=microservices-demo:helmrelease/frontend helmVersion=v3 info="starting sync run"
ts=2021-03-08T15:58:43.600219591Z caller=release.go:289 component=release release=frontend targetNamespace=microservices-demo resource=microservices-demo:helmrelease/frontend helmVersion=v3 info="running dry-run upgrade to compare with release version '2'" action=dry-run-compare
ts=2021-03-08T15:58:43.603927908Z caller=helm.go:69 component=helm version=v3 info="preparing upgrade for frontend" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:43.608666281Z caller=helm.go:69 component=helm version=v3 info="resetting values to the chart's original version" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:44.042624789Z caller=helm.go:69 component=helm version=v3 info="performing update for frontend" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:44.166902171Z caller=helm.go:69 component=helm version=v3 info="dry run for frontend" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:44.188489685Z caller=release.go:311 component=release release=frontend targetNamespace=microservices-demo resource=microservices-demo:helmrelease/frontend helmVersion=v3 info="no changes" phase=dry-run-compare
ts=2021-03-08T15:58:45.512229733Z caller=release.go:79 component=release release=frontend targetNamespace=microservices-demo resource=microservices-demo:helmrelease/frontend helmVersion=v3 info="starting sync run"
ts=2021-03-08T15:58:45.900728191Z caller=release.go:353 component=release release=frontend targetNamespace=microservices-demo resource=microservices-demo:helmrelease/frontend helmVersion=v3 info="running upgrade" action=upgrade
ts=2021-03-08T15:58:45.948627111Z caller=helm.go:69 component=helm version=v3 info="preparing upgrade for frontend" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:45.958203638Z caller=helm.go:69 component=helm version=v3 info="resetting values to the chart's original version" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:46.336755783Z caller=helm.go:69 component=helm version=v3 info="performing update for frontend" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:46.411455978Z caller=helm.go:69 component=helm version=v3 info="creating upgraded release for frontend" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:46.450067098Z caller=helm.go:69 component=helm version=v3 info="checking 4 resources for changes" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:46.458534823Z caller=helm.go:69 component=helm version=v3 info="Looks like there are no changes for Service \"frontend\"" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:46.477010619Z caller=helm.go:69 component=helm version=v3 info="Looks like there are no changes for Deployment \"frontend\"" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:46.491257633Z caller=helm.go:69 component=helm version=v3 info="Looks like there are no changes for Gateway \"frontend-gateway\"" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:46.509866554Z caller=helm.go:69 component=helm version=v3 info="Looks like there are no changes for VirtualService \"frontend\"" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:46.521888271Z caller=helm.go:69 component=helm version=v3 info="updating status for upgraded release for frontend" targetNamespace=microservices-demo release=frontend
ts=2021-03-08T15:58:46.566017666Z caller=release.go:364 component=release release=frontend targetNamespace=microservices-demo resource=microservices-demo:helmrelease/frontend helmVersion=v3 info="upgrade succeeded" revision=dabfe09c1e6f9f4c187c9875acd3c630fc86af71 phase=upgrade`
- [V] * Установлен istio с помощью istio operator:
`istioctl operator init`;
`Установка istio из default профиля :
kubectl create ns istio-system
kubectl apply -f - <<EOF
apiVersion: install.istio.io/v1alpha1
kind: IstioOperator
metadata:
  namespace: istio-system
  name: example-istiocontrolplane
spec:
  profile: default
EOF`
- [V] Установлен flagger - вышла новая api - flagger.app/v1beta1 -в ней появился ряд изменений,в связи с которыми пришлось переделать пример конфига из домашки -приложил свой конфиг - flagger/canary.yml :
>the spec.canaryAnalysis field has been deprecated and replaced with spec.analysis
>the spec.analysis.interval and spec.analysis.threshold fields are required
- [V] Добавлен  Sidecar Injection и сделан istio-ingress,манифесты добавлены как шаблоны в чарт frontend
- [V] Сделан новый релиз,запущен loadgenerator с указанием правильного ip - http://35.228.60.147/ -произведен успешный релиз frontend:
` major@MacBook-Air  ~  kubectl get canaries
NAME       STATUS      WEIGHT   LASTTRANSITIONTIME
frontend   Succeeded   0        2021-03-11T18:10:48Z`


`⚙ major@MacBook-Air  ~  kubectl describe canary -n frontend -n microservices-demo
Name:         frontend
Namespace:    microservices-demo
Labels:       app.kubernetes.io/managed-by=Helm
Annotations:  helm.fluxcd.io/antecedent: microservices-demo:helmrelease/frontend
              meta.helm.sh/release-name: frontend
              meta.helm.sh/release-namespace: microservices-demo
API Version:  flagger.app/v1beta1
Kind:         Canary
Metadata:
  Creation Timestamp:  2021-03-11T17:37:07Z
  Generation:          2
  Managed Fields:
    API Version:  flagger.app/v1beta1
    Fields Type:  FieldsV1
    fieldsV1:
      f:metadata:
        f:annotations:
          .:
          f:helm.fluxcd.io/antecedent:
    Manager:      kubectl
    Operation:    Update
    Time:         2021-03-11T17:37:09Z
    API Version:  flagger.app/v1beta1
    Fields Type:  FieldsV1
    fieldsV1:
      f:spec:
        f:service:
          f:portDiscovery:
      f:status:
        .:
        f:canaryWeight:
        f:conditions:
        f:failedChecks:
        f:iterations:
        f:lastAppliedSpec:
        f:lastTransitionTime:
        f:phase:
        f:trackedConfigs:
    Manager:      flagger
    Operation:    Update
    Time:         2021-03-11T17:38:08Z
    API Version:  flagger.app/v1beta1
    Fields Type:  FieldsV1
    fieldsV1:
      f:metadata:
        f:annotations:
          f:meta.helm.sh/release-name:
          f:meta.helm.sh/release-namespace:
        f:labels:
          .:
          f:app.kubernetes.io/managed-by:
      f:spec:
        .:
        f:analysis:
          .:
          f:interval:
          f:iterations:
          f:threshold:
        f:provider:
        f:service:
          .:
          f:gateways:
          f:hosts:
          f:port:
          f:targetPort:
          f:trafficPolicy:
            .:
            f:tls:
              .:
              f:mode:
        f:targetRef:
          .:
          f:apiVersion:
          f:kind:
          f:name:
    Manager:         Go-http-client
    Operation:       Update
    Time:            2021-03-11T17:43:18Z
  Resource Version:  5378708
  Self Link:         /apis/flagger.app/v1beta1/namespaces/microservices-demo/canaries/frontend
  UID:               bc054f6a-0fae-4c5c-9070-07dd33a3a2b2
Spec:
  Analysis:
    Interval:    30s
    Iterations:  3
    Threshold:   10
  Provider:      istio
  Service:
    Gateways:
      frontend
    Hosts:
      35.228.60.147
    Port:         80
    Target Port:  8080
    Traffic Policy:
      Tls:
        Mode:  DISABLE
  Target Ref:
    API Version:  apps/v1
    Kind:         Deployment
    Name:         frontend
Status:
  Canary Weight:  0
  Conditions:
    Last Transition Time:  2021-03-11T18:10:48Z
    Last Update Time:      2021-03-11T18:10:48Z
    Message:               Canary analysis completed successfully, promotion finished.
    Reason:                Succeeded
    Status:                True
    Type:                  Promoted
  Failed Checks:           0
  Iterations:              0
  Last Applied Spec:       668cdf9588
  Last Transition Time:    2021-03-11T18:10:48Z
  Phase:                   Succeeded
  Tracked Configs:
Events:  <none>`
## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>