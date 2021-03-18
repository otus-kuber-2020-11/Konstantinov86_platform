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

<details><summary>ДЗ №11</summary>

 - [V] Основное ДЗ
 - [] Задание со *
## В процессе сделано:
- [V] Установлен vault и consul:
```
helm status vault
NAME: vault
LAST DEPLOYED: Wed Mar 17 16:39:04 2021
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Thank you for installing HashiCorp Vault!

Now that you have deployed Vault, you should look over the docs on using
Vault with Kubernetes available here:

https://www.vaultproject.io/docs/


Your release is named vault. To learn more about the release, try:

  $ helm status vault
  $ helm get manifest vault"

```
- [V]  инициализация ключей:
```
vault operator init --key-shares=1 --key-threshold=1
Unseal Key 1: w5l3gwMhZoYPvvU0d8PPFVj3OPuO/IMriOa9oEFn1uQ=

Initial Root Token: s.05dV37GkrjVSSg7q8ZtpYHyC

Vault initialized with 1 key shares and a key threshold of 1. Please securely
distribute the key shares printed above. When the Vault is re-sealed,
restarted, or stopped, you must supply at least 1 of these keys to unseal it
before it can start servicing requests.

Vault does not store the generated master key. Without at least 1 key to
reconstruct the master key, Vault will remain permanently sealed!

It is possible to generate new unseal keys, provided you have a quorum of
existing unseal keys shares. See "vault operator rekey" for more information.`

```
- [V] Unseal подов:
```
Key             Value
---             -----
Seal Type       shamir
Initialized     true
Sealed          false
Total Shares    1
Threshold       1
Version         1.6.2
Storage Type    consul
Cluster Name    vault-cluster-9c25cec9
Cluster ID      7aaa00fb-2c8b-b74e-f8c7-529afa24b899
HA Enabled      true
HA Cluster      https://vault-0.vault-internal:8201
HA Mode         active
- [V] login:
Success! You are now authenticated. The token information displayed below
is already stored in the token helper. You do NOT need to run "vault login"
again. Future Vault requests will automatically use this token.

Key                  Value
---                  -----
token                s.05dV37GkrjVSSg7q8ZtpYHyC
token_accessor       tM5BMDAZLF7fTGYkprwDyOVV
token_duration       ∞
token_renewable      false
token_policies       ["root"]
identity_policies    []
policies             ["root"]
```
- [V] auth list:
```
Path      Type     Accessor               Description
----      ----     --------               -----------
token/    token    auth_token_40540e1d    token based credentials
- [V] Завели секреты:
key                 Value
---                 -----
refresh_interval    768h
password            asajkjkahs
username            otus`
```
- [V] Включил авторизацию K8S :
```
Path           Type          Accessor                    Description
----           ----          --------                    -----------
kubernetes/    kubernetes    auth_kubernetes_d2cb5f5c    n/a
token/         token         auth_token_40540e1d         token based credentials`
```
- [V] Создали  service account  с  clusterrolebinding;
- [V] создали файл политики и ролей и записали в  vault;
- [V] Провели проверку политик - Не смогли записать otus-rw/config потому что в политиках ранее не указали разрешение на update:
```
path "otus/otus-rw/*" {
capabilities = ["read", "create", "list","update"]`
```
- [V] Скопировали vault-agent-k8s-demo из репозитория vault-guides и скорректировал конфиги с учетом ранее
созданых ролей и секретов  -  config-k8s/example-k8-spec.yaml  и  configmap.yaml
- [V] Запустили под и проверили  index.html :
```
cat index.html
<html>
<body>
<p>Some secrets:</p>
<ul>
<li><pre>username: otus</pre></li>
<li><pre>password: asajkjkahs</pre></li>
</ul>

</body>
</html>`
```

- [V] Включили pki секретс и подписали урлы;
- [V] создали промежуточный сертификат и прописали его в vault;
- [V] Создали и отозвали сертификат:
'
```
Key                 Value
---                 -----
ca_chain            [-----BEGIN CERTIFICATE-----
MIIDnDCCAoSgAwIBAgIUDKudU/Hz+k6R9K09W7+SipjFZOYwDQYJKoZIhvcNAQEL
BQAwFTETMBEGA1UEAxMKZXhhbXBsZS5ydTAeFw0yMTAzMTcxODEzNDdaFw0yNjAz
MTYxODE0MTdaMCwxKjAoBgNVBAMTIWV4YW1wbGUucnUgSW50ZXJtZWRpYXRlIEF1
dGhvcml0eTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBALwB64cD8ZF3
/S7FFdSyP5VhCDg0KCCLFT90NpyfO6bazMVBE0ZaTr8EMBEf+OMP3yfZnSe+k35R
Xuh3Zmc44QzQjjbaniYyo5R6pmU5a4G4Qer2xr8owQdKa6ga+iOkR5WBrR9oT6Zo
6Cz/xQTHXw76mEqewnVOzwiaDtUOD0LBzh29c3n9iISs17xCLtqj+fIB53/gXP7t
GaTWoosOKNt5YNZymhukQogsWqiqQ8Oqg8G2AKgVX1fzzUKam9ysyEXMzmOvb5qw
F6pSZWksEna8eJIKNfF87PYRL4R5DKlojpxAtJxJxKKUR0RwHcSSN1L6GpLLuJzh
0VEU061eUmUCAwEAAaOBzDCByTAOBgNVHQ8BAf8EBAMCAQYwDwYDVR0TAQH/BAUw
AwEB/zAdBgNVHQ4EFgQU47WRdeilIgXRWtDqLkj6S8TMtkEwHwYDVR0jBBgwFoAU
2pvAhkyW9WZQaAe+94jnsvedELgwNwYIKwYBBQUHAQEEKzApMCcGCCsGAQUFBzAC
hhtodHRwOi8vdmF1bHQ6ODIwMC92MS9wa2kvY2EwLQYDVR0fBCYwJDAioCCgHoYc
aHR0cDovL3ZhdWx0OjgyMDAvdjEvcGtpL2NybDANBgkqhkiG9w0BAQsFAAOCAQEA
P+WTOjdf/N/U4n4MGndU1bSSXWyUo/9E3YiqGp4hmZtBveoQ0lXY1R0/scKkFjuw
mksphWeBRFUfust8ZlSFaJMpRk6ccPjopLwX6Ap5PVKuqFzmq4MWiIqCtndry7pL
0BPxsNPPAo23474TUBCeYz61xueqLbZEGosGNxEelR2tj57QSTOSqPjcOpnmSe8T
1k07Q+TCVBe0qJqT3/20G9idPMXGYoUheL51v2L3ndvpY+XL+DAHDzQNsxr99uGP
3TrUcIpbmfKkLBGZK1y8tyNZ0JlOrGHwfjfXphX9irs6XxMbbi56B5EVB31f/DdE
DuCFIsPBZboCwDzywr6xYA==
-----END CERTIFICATE-----]
certificate         -----BEGIN CERTIFICATE-----
MIIDZzCCAk+gAwIBAgIUS4NEFzQgMRGfriQIaukwrzDfFYMwDQYJKoZIhvcNAQEL
BQAwLDEqMCgGA1UEAxMhZXhhbXBsZS5ydSBJbnRlcm1lZGlhdGUgQXV0aG9yaXR5
MB4XDTIxMDMxNzE4MTgwMFoXDTIxMDMxODE4MTgzMFowHDEaMBgGA1UEAxMRZ2l0
bGFiLmV4YW1wbGUucnUwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC7
kD+afSamJb1O+AsxZBYnWb1GthVVisYU1WbHzwduenYOXX3G13XMr1Ifo7tkkxGa
+36ALVte23XCIHP0P3Q2XUo08pFaYdMBxYu2GvTUWZS+ohZyngBXRJCoyhTS6+li
dx736efR0bAe2nVr6JJrMh6jZzu3/Rtn3jrOJd3zboCUo/G9WMbZKY+0WpIufZtf
X+6/WAyaCnqrCsv5IDgMcpZq3tVrncR4ZyKj27iAwEvHVrEpkPbASaS8KcpTiSXd
aFaXzaR/2Ad+MwgrCtBWzpHwRuyLePFuExrp0RqaX8FZ/INRJ2zt9mGcMFb1nRvq
5FR2XNN4tVfr8jR8YQjBAgMBAAGjgZAwgY0wDgYDVR0PAQH/BAQDAgOoMB0GA1Ud
JQQWMBQGCCsGAQUFBwMBBggrBgEFBQcDAjAdBgNVHQ4EFgQUl9E8gxgQU384jCUk
iIYbTX9SrfwwHwYDVR0jBBgwFoAU47WRdeilIgXRWtDqLkj6S8TMtkEwHAYDVR0R
BBUwE4IRZ2l0bGFiLmV4YW1wbGUucnUwDQYJKoZIhvcNAQELBQADggEBAH9WV9oG
OXIpu+ay5tl/mWaB5/NniHuoSUqHn+CVtZGCC2zERdAGa0ELNTqiZ5eSrowzu2La
2rZIN/rUrZrbJgpyN9mIDRBMYBDtmGLgGEbGdynslCTvTGS5g/AKYpmAqT87By+W
3QEOJUdc+T7HBqLYNt1Tbh5s43166UogMD9m27xvLWkNLbg4pYi22jBOYJyEvYB/
sBhFNFlXwp6Ngzsp7SsUKg3ukRlZlg6fASjpx2ka6wNri5Cbd6frTdfcPJc/dWTh
sOg1PXqqFFngHhYfAqgKwOAgR9v2qfOSHyHjVtmP5fOD23VCrWOgmV9EMWfhra47
OtYwT69DBq0EaFE=
-----END CERTIFICATE-----
expiration          1616091510
issuing_ca          -----BEGIN CERTIFICATE-----
MIIDnDCCAoSgAwIBAgIUDKudU/Hz+k6R9K09W7+SipjFZOYwDQYJKoZIhvcNAQEL
BQAwFTETMBEGA1UEAxMKZXhhbXBsZS5ydTAeFw0yMTAzMTcxODEzNDdaFw0yNjAz
MTYxODE0MTdaMCwxKjAoBgNVBAMTIWV4YW1wbGUucnUgSW50ZXJtZWRpYXRlIEF1
dGhvcml0eTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBALwB64cD8ZF3
/S7FFdSyP5VhCDg0KCCLFT90NpyfO6bazMVBE0ZaTr8EMBEf+OMP3yfZnSe+k35R
Xuh3Zmc44QzQjjbaniYyo5R6pmU5a4G4Qer2xr8owQdKa6ga+iOkR5WBrR9oT6Zo
6Cz/xQTHXw76mEqewnVOzwiaDtUOD0LBzh29c3n9iISs17xCLtqj+fIB53/gXP7t
GaTWoosOKNt5YNZymhukQogsWqiqQ8Oqg8G2AKgVX1fzzUKam9ysyEXMzmOvb5qw
F6pSZWksEna8eJIKNfF87PYRL4R5DKlojpxAtJxJxKKUR0RwHcSSN1L6GpLLuJzh
0VEU061eUmUCAwEAAaOBzDCByTAOBgNVHQ8BAf8EBAMCAQYwDwYDVR0TAQH/BAUw
AwEB/zAdBgNVHQ4EFgQU47WRdeilIgXRWtDqLkj6S8TMtkEwHwYDVR0jBBgwFoAU
2pvAhkyW9WZQaAe+94jnsvedELgwNwYIKwYBBQUHAQEEKzApMCcGCCsGAQUFBzAC
hhtodHRwOi8vdmF1bHQ6ODIwMC92MS9wa2kvY2EwLQYDVR0fBCYwJDAioCCgHoYc
aHR0cDovL3ZhdWx0OjgyMDAvdjEvcGtpL2NybDANBgkqhkiG9w0BAQsFAAOCAQEA
P+WTOjdf/N/U4n4MGndU1bSSXWyUo/9E3YiqGp4hmZtBveoQ0lXY1R0/scKkFjuw
mksphWeBRFUfust8ZlSFaJMpRk6ccPjopLwX6Ap5PVKuqFzmq4MWiIqCtndry7pL
0BPxsNPPAo23474TUBCeYz61xueqLbZEGosGNxEelR2tj57QSTOSqPjcOpnmSe8T
1k07Q+TCVBe0qJqT3/20G9idPMXGYoUheL51v2L3ndvpY+XL+DAHDzQNsxr99uGP
3TrUcIpbmfKkLBGZK1y8tyNZ0JlOrGHwfjfXphX9irs6XxMbbi56B5EVB31f/DdE
DuCFIsPBZboCwDzywr6xYA==
-----END CERTIFICATE-----
private_key         -----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAu5A/mn0mpiW9TvgLMWQWJ1m9RrYVVYrGFNVmx88Hbnp2Dl19
xtd1zK9SH6O7ZJMRmvt+gC1bXtt1wiBz9D90Nl1KNPKRWmHTAcWLthr01FmUvqIW
cp4AV0SQqMoU0uvpYnce9+nn0dGwHtp1a+iSazIeo2c7t/0bZ946ziXd826AlKPx
vVjG2SmPtFqSLn2bX1/uv1gMmgp6qwrL+SA4DHKWat7Va53EeGcio9u4gMBLx1ax
KZD2wEmkvCnKU4kl3WhWl82kf9gHfjMIKwrQVs6R8Ebsi3jxbhMa6dEaml/BWfyD
USds7fZhnDBW9Z0b6uRUdlzTeLVX6/I0fGEIwQIDAQABAoIBAFdS4Unb2pKgH3MU
qKFmJ6pKbYTuYSBia7ZnZGLCUINvIGevv09EIOQa+/EfGa/JiPjO/iZO96tCIaEv
2sxsfn6REGt2Q5YA1WyNvG4cPsBetJHMhQb36NC4a2EqNGe+zfm53AEwNW3KYmT6
8JA8x26A9yK8fWE7xfal0FsJ5jve+lSufKVWuFw6FDXyUhxKucSucMSLRN4d/64y
p3OumW/aQgOTWeeESAuPlHlhRIgsMhAOkYOoEvW+XPYkXWM0KVWuIb1oHY4XPcOC
sWRp3e/RzNrrtroSxESHVATQ7N+pRU6VuFLnvJANlcWv289CdNGa3ZYA7PNveUQa
fqkJsMECgYEA0JiCi0d/ZPW2KoJIYmRxBlx3fGF953lnJ5eWNk6SfT9xInWaJfJh
dnYjfmFBUhgTYOxtbm/pJkPeAj3L8c8TV+1Nfrf+OIQvMThJlIilh1HbHiMuGgYZ
aMAPtyApTQcoz906gtnToyeftDIei17rb3LWP6W2O/WiYpTMy0c6HkcCgYEA5jAk
egcSL6g6vcuW4nozmIGytEEoVE1RDW+pBqUiF3DibWX8nlVoeV7T0UpXS+JK+ArU
kvvBquqfS5ngB/nGYPwfv3rHAb7OumUNYzJ6NRH5hWoWqSA1h63IHgObTefetFdY
kE0sumfhkbukPbO0dWVDhDqUlB6OfSnf/An9fLcCgYAtV9mYuRQCOD8/Ak8FxFul
TFhU20RpGsTHoHXwnCfPvgizuuilMwjonUmd4To3xDACM6KeDQmbXclWp2Q7zg2g
YV8lGo3Sbzlq85dbCFEjFzIQXQlactT3JjjET+NqcRH4DVj4tK0CnExk+TgWh62Z
7laQQ09XvU9tKndSAMurZQKBgGPRLpAn7s/xsH9LAIP3H9abL2YQ9y8PU/1ylSZH
h3AIyHdOCWyTdrli0JFqHk7Os1m6QJH4T/QQx8Dd2hM7UbYOvqmm0RNFrZmQZmzE
n8/RmpUq+uaeC/ho+GVjhP4UdTNYyRPSE3pFv8AVUVRcT/20SsHVMUbFtV47QWCm
6GAjAoGAZav1DxNz9DAIQpw5kW40UMM7Pk++jWvXsCVKsiXcYUc2tboKAt4WN4Pj
oqpUNskjE7+98/6yq0yvCKdB89zfO3cmlKueizMfW6ezBix1uoNAHZzk59/cc/Ke
yceL3hEcIx5RuPmIO2WDDKqKnI2urA2T3nxu8hSEUS4jYVV/sGI=
-----END RSA PRIVATE KEY-----
private_key_type    rsa
serial_number       4b:83:44:17:34:20:31:11:9f:ae:24:08:6a:e9:30:af:30:df:15:83''


```
## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>

<details><summary>ДЗ № 12</summary>

 - [V] Основное ДЗ
 - [ ] Задание со *

## В процессе сделано:
- [V] Создал CRD и snapshot-controller - kubectl apply -f crd_volumesnapshot;
- [V] Задеплоил csi-driver-host-path - kubectl apply -f hostpath :
```
NAME                         READY   STATUS    RESTARTS   AGE
csi-hostpath-attacher-0      1/1     Running   0          7s
csi-hostpath-provisioner-0   1/1     Running   0          6s
csi-hostpath-resizer-0       1/1     Running   0          6s
csi-hostpath-snapshotter-0   1/1     Running   0          6s
csi-hostpath-socat-0         1/1     Running   0          6s
csi-hostpathplugin-0         5/5     Running   0          6s
snapshot-controller-0        1/1     Running   0          13s
```
- [V] Создал POD StorageClass и PVC - kubectl apply  -f csi-app_pvc:
```
NAME      STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS      AGE
csi-pvc   Bound    pvc-cb32f65b-912c-4183-950c-8c13102eba82   1Gi        RWO            csi-hostpath-sc   1m
```
- [V] Запишем в pvc :
```
kubectl exec -it my-csi-app /bin/sh
/ # touch /data/hello-world
/ # exit
```
- [V] Проверим что  файл есть :
```
kubectl exec -it $(kubectl get pods --selector app=csi-hostpathplugin -o jsonpath='{.items[*].metadata.name}') -c hostpath /bin/sh
/ # find / -name hello-world
/csi-data-dir/853cf954-8808-11eb-922f-36e61f069e21/hello-world
```
- [V]Установим volumesnapshotclass - kubectl apply -f snapshotter:
```
kubectl get volumesnapshotclass
NAME                     AGE
csi-hostpath-snapclass   3s
```
- [V] Создадим снэпшот - kubectl apply -f csi-snapshot-v1beta1.yaml:
```
kubectl get volumesnapshot
NAME                AGE
new-snapshot-demo   69s
```
- [V] Удаляем POD и PVC
- [V] Восстанавливаем snapshot - kubectl apply -g csi-restore.yaml:
```
kubectl get pvc
NAME           STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS      AGE
hpvc-restore   Bound    pvc-23810ee6-4e62-4e13-917b-aec10011b6c6   1Gi        RWO            csi-hostpath-sc   80s
```
- [V] Проверяем что  файл есть :
```
kubectl exec -it my-csi-app /bin/sh
/ # ls /data/
/ # hello-world
```## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>