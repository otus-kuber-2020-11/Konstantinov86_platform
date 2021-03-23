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
- [V] Восстанавливаем snapshot - kubectl apply -f csi-restore.yaml:
```
kubectl get pvc
NAME           STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS      AGE
hpvc-restore   Bound    pvc-23810ee6-4e62-4e13-917b-aec10011b6c6   1Gi        RWO            csi-hostpath-sc   80s
```
- [V] запускаем под kubectl apply -f csi-app.yaml
- [V] Проверяем что  файл есть :
```
kubectl exec -it my-csi-app /bin/sh
/ # ls /data/
/ # hello-world
```
## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>

 <details><summary>ДЗ № 13</summary>

 - [V] Основное ДЗ
 - [ ] Задание со *

- [V] Работа c kubectl-debug:
Не работает strace ,потому что необходимо добавлять разрешения для ptrace в контейнере  --cap-add=SYS_PTRACE (в Docker 19.3 системные вызовы ptrace разрешены);
В манифесте kubectl-debug  из ДЗ стоит версия дебаг пода -  0.0.1 ,где  не выставлено данное разрешение;
Можно  заменить на версию 0.1.1 где применен данный коммит:
```
		UsernsMode:  container.UsernsMode(m.containerMode(targetId)),
		IpcMode:     container.IpcMode(m.containerMode(targetId)),
		PidMode:     container.PidMode(m.containerMode(targetId)),
		CapAdd:      strslice.StrSlice([]string{"SYS_PTRACE", "SYS_ADMIN"}),
	}
	ctx, cancel := m.getContextWithTimeout()
	defer cancel()
  ```
- [V] установил оператор netperf-operator и тестовый cr kubectl apply -f /kit/deploy-netperf:
```
Name:         example
Namespace:    test
Labels:       <none>
Annotations:  <none>
API Version:  app.example.com/v1alpha1
Kind:         Netperf
Metadata:
  Creation Timestamp:  2021-03-21T13:37:20Z
  Generation:          4
  Managed Fields:
    API Version:  app.example.com/v1alpha1
    Fields Type:  FieldsV1
    fieldsV1:
      f:metadata:
        f:annotations:
          .:
          f:kubectl.kubernetes.io/last-applied-configuration:
    Manager:      kubectl-client-side-apply
    Operation:    Update
    Time:         2021-03-21T13:37:20Z
    API Version:  app.example.com/v1alpha1
    Fields Type:  FieldsV1
    fieldsV1:
      f:spec:
        .:
        f:clientNode:
        f:serverNode:
      f:status:
        .:
        f:clientPod:
        f:serverPod:
        f:speedBitsPerSec:
        f:status:
    Manager:         netperf-operator
    Operation:       Update
    Time:            2021-03-21T13:37:20Z
  Resource Version:  1736749
  Self Link:         /apis/app.example.com/v1alpha1/namespaces/test/netperfs/example
  UID:               195e3ad8-9c3e-4750-8b54-f21dbc2b464a
Spec:
  Client Node:
  Server Node:
Status:
  Client Pod:          netperf-client-f21dbc2b464a
  Server Pod:          netperf-server-f21dbc2b464a
  Speed Bits Per Sec:  1875.14
  Status:              Done
Events:                <none>
```
- [V] Добавляем сетевую политику calico -  kubectl apply -f netperf-calico-policy.yaml:
```
sudo iptables --list -nv | grep LOG
    0     0 LOG        all  --  *      *       0.0.0.0/0            0.0.0.0/0            /* cali:XWC9Bycp2Xf7yVk1 */ LOG flags 0 level 5 prefix "calico-packet: "
    9   540 LOG        all  --  *      *       0.0.0.0/0            0.0.0.0/0            /* cali:B30DykF1ntLW86eD */ LOG flags 0 level 5 prefix "calico-packet: "
```
- [V] Запускаем iptables-tailer, kubectl apply -f iptables-tailer.yaml -( необходимо доработать предоставленный манифест так как extensions/v1beta1 deprecated ):
- [V] Появились ошибки account :
````
kube-system   4m5s        Warning   FailedCreate        daemonset/kube-iptables-tailer                 Error creating: pods "kube-iptables-tailer-" is forbidden: error looking up service account kube-system/kube-iptables-tailer: serviceaccount "kube-iptables-tailer" not found
````
Создадим SA -kubectl apply  -f sa.yaml;
- [V] Изменим префикс PTABLES_LOG_PREFIX на calico-packet и  JOURNAL_DIRECTORY на /var/log/journal;
- [V] Перезапустим тесты и увидим результат :
```
Events:
  Type     Reason      Age   From                  Message
  ----     ------      ----  ----                  -------
  Normal   Scheduled   26s   default-scheduler     Successfully assigned test/netperf-server-36acf46d0825 to gke-serious-energy-serious-energy-nod-9289b5e6-igkc
  Normal   Pulling     25s   kubelet               Pulling image "tailoredcloud/netperf:v2.7"
  Normal   Pulled      22s   kubelet               Successfully pulled image "tailoredcloud/netperf:v2.7"
  Normal   Created     22s   kubelet               Created container netperf-server-36acf46d0825
  Normal   Started     22s   kubelet               Started container netperf-server-36acf46d0825
  Warning  PacketDrop  18s   kube-iptables-tailer  Packet dropped when receiving traffic from 10.84.2.10
  ```
## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>

<details><summary>ДЗ № 14</summary>

 - [V] Основное ДЗ
 - [ ] Задание со *

## В процессе сделано:
- [V] В GCP создал 4 ноды с образом Ubuntu 18.04 LTS:
 ```
 template-for-master-1	europe-north1-a	10.166.0.31 (nic0)	35.228.204.142 	 	
 template-for-worker-1	europe-north1-a	10.166.0.32 (nic0)	35.228.182.231 	 	
 template-for-worker-2	europe-north1-a	10.166.0.33 (nic0)	35.228.60.147 	 	
 template-for-worker-3	europe-north1-a	10.166.0.34 (nic0)	35.228.126.189
 ```	

- [V] Установил ПО и произвел kubeadm init :
```
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 10.166.0.31:6443 --token h9c9x9.yn6c5pq66nsagaqz \
    --discovery-token-ca-cert-hash sha256:b9a23cb6c768905b762593a9d9e2336a1de1e6cec8fd2ebc0e12a6906982d95e
```

```
NAME                    STATUS   ROLES    AGE   VERSION
template-for-master-1   Ready    master   11m   v1.17.4
```


- [V] Заджоинил остальные ноды :
```
root@template-for-master-1:~# kubectl get nodes
NAME                    STATUS   ROLES    AGE   VERSION
template-for-master-1   Ready    master   16m   v1.17.4
template-for-worker-1   Ready    <none>   65s   v1.17.4
template-for-worker-2   Ready    <none>   62s   v1.17.4
template-for-worker-3   Ready    <none>   57s   v1.17.4
```
- [V] Задеплоил nginx:
```
root@template-for-master-1:~# kubectl get pods -o wide
NAME                               READY   STATUS    RESTARTS   AGE   IP              NODE                    NOMINATED NODE   READINESS GATES
nginx-deployment-c8fd555cc-8vkdw   1/1     Running   0          19s   192.168.0.65    template-for-worker-1   <none>           <none>
nginx-deployment-c8fd555cc-9hkmg   1/1     Running   0          19s   192.168.0.2     template-for-worker-2   <none>           <none>
nginx-deployment-c8fd555cc-qvr88   1/1     Running   0          19s   192.168.0.1     template-for-worker-2   <none>           <none>
nginx-deployment-c8fd555cc-s6zs2   1/1     Running   0          19s   192.168.0.129   template-for-worker-3   <none>
```
- [V] Обновил kubectl:
```
root@template-for-master-1:~# kubectl get nodes
NAME                    STATUS   ROLES    AGE     VERSION
template-for-master-1   Ready    master   23m     v1.18.0
template-for-worker-1   Ready    <none>   8m15s   v1.17.4
template-for-worker-2   Ready    <none>   8m12s   v1.17.4
template-for-worker-3   Ready    <none>   8m7s    v1.17.4
```
- [V]Провел upgrade:
```
root@template-for-master-1:~# kubeadm upgrade plan
[upgrade/config] Making sure the configuration is correct:
[upgrade/config] Reading configuration from the cluster...
[upgrade/config] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -oyaml'
[preflight] Running pre-flight checks.
[upgrade] Running cluster health checks
[upgrade] Fetching available versions to upgrade to
[upgrade/versions] Cluster version: v1.17.17
[upgrade/versions] kubeadm version: v1.18.0
I0323 18:02:25.720194   10558 version.go:252] remote version is much newer: v1.20.5; falling back to: stable-1.18
[upgrade/versions] Latest stable version: v1.18.17
[upgrade/versions] Latest stable version: v1.18.17
[upgrade/versions] Latest version in the v1.17 series: v1.17.17
[upgrade/versions] Latest version in the v1.17 series: v1.17.17

Components that must be upgraded manually after you have upgraded the control plane with 'kubeadm upgrade apply':
COMPONENT   CURRENT       AVAILABLE
Kubelet     3 x v1.17.4   v1.18.17
            1 x v1.18.0   v1.18.17

Upgrade to the latest stable version:

COMPONENT            CURRENT    AVAILABLE
API Server           v1.17.17   v1.18.17
Controller Manager   v1.17.17   v1.18.17
Scheduler            v1.17.17   v1.18.17
Kube Proxy           v1.17.17   v1.18.17
CoreDNS              1.6.5      1.6.7
Etcd                 3.4.3      3.4.3-0

You can now apply the upgrade by executing the following command:

	kubeadm upgrade apply v1.18.17

Note: Before you can perform this upgrade, you have to update kubeadm to v1.18.17.

_____________________________________________________________________

root@template-for-master-1:~# kubeadm upgrade apply v1.18.0
[upgrade/config] Making sure the configuration is correct:
[upgrade/config] Reading configuration from the cluster...
[upgrade/config] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -oyaml'
[preflight] Running pre-flight checks.
[upgrade] Running cluster health checks
[upgrade/version] You have chosen to change the cluster version to "v1.18.0"
[upgrade/versions] Cluster version: v1.17.17
[upgrade/versions] kubeadm version: v1.18.0
[upgrade/confirm] Are you sure you want to proceed with the upgrade? [y/N]: y
[upgrade/prepull] Will prepull images for components [kube-apiserver kube-controller-manager kube-scheduler etcd]
[upgrade/prepull] Prepulling image for component etcd.
[upgrade/prepull] Prepulling image for component kube-apiserver.
[upgrade/prepull] Prepulling image for component kube-controller-manager.
[upgrade/prepull] Prepulling image for component kube-scheduler.
[apiclient] Found 1 Pods for label selector k8s-app=upgrade-prepull-kube-scheduler
[apiclient] Found 1 Pods for label selector k8s-app=upgrade-prepull-kube-controller-manager
[apiclient] Found 1 Pods for label selector k8s-app=upgrade-prepull-kube-apiserver
[apiclient] Found 0 Pods for label selector k8s-app=upgrade-prepull-etcd
[apiclient] Found 1 Pods for label selector k8s-app=upgrade-prepull-etcd
[upgrade/prepull] Prepulled image for component etcd.
[upgrade/prepull] Prepulled image for component kube-apiserver.
[upgrade/prepull] Prepulled image for component kube-scheduler.
[upgrade/prepull] Prepulled image for component kube-controller-manager.
[upgrade/prepull] Successfully prepulled the images for all the control plane components
[upgrade/apply] Upgrading your Static Pod-hosted control plane to version "v1.18.0"...
Static pod: kube-apiserver-template-for-master-1 hash: dca0ec96c1010ef7509ea293180e0334
Static pod: kube-controller-manager-template-for-master-1 hash: c43b349fe40aab07b8e29b4a2be8c4af
Static pod: kube-scheduler-template-for-master-1 hash: d2768f36096b01759dbdef9ca638ffd0
[upgrade/etcd] Upgrading to TLS for etcd
[upgrade/etcd] Non fatal issue encountered during upgrade: the desired etcd version for this Kubernetes version "v1.18.0" is "3.4.3-0", but the current etcd version is "3.4.3". Won't downgrade etcd, instead just continue
[upgrade/staticpods] Writing new Static Pod manifests to "/etc/kubernetes/tmp/kubeadm-upgraded-manifests758490787"
W0323 18:04:09.996066   11825 manifests.go:225] the default kube-apiserver authorization-mode is "Node,RBAC"; using "Node,RBAC"
[upgrade/staticpods] Preparing for "kube-apiserver" upgrade
[upgrade/staticpods] Renewing apiserver certificate
[upgrade/staticpods] Renewing apiserver-kubelet-client certificate
[upgrade/staticpods] Renewing front-proxy-client certificate
[upgrade/staticpods] Renewing apiserver-etcd-client certificate
[upgrade/staticpods] Moved new manifest to "/etc/kubernetes/manifests/kube-apiserver.yaml" and backed up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2021-03-23-18-04-09/kube-apiserver.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This might take a minute or longer depending on the component/version gap (timeout 5m0s)
Static pod: kube-apiserver-template-for-master-1 hash: dca0ec96c1010ef7509ea293180e0334
Static pod: kube-apiserver-template-for-master-1 hash: dca0ec96c1010ef7509ea293180e0334
Static pod: kube-apiserver-template-for-master-1 hash: dca0ec96c1010ef7509ea293180e0334
Static pod: kube-apiserver-template-for-master-1 hash: dca0ec96c1010ef7509ea293180e0334
Static pod: kube-apiserver-template-for-master-1 hash: dca0ec96c1010ef7509ea293180e0334
Static pod: kube-apiserver-template-for-master-1 hash: dca0ec96c1010ef7509ea293180e0334
Static pod: kube-apiserver-template-for-master-1 hash: dca0ec96c1010ef7509ea293180e0334
Static pod: kube-apiserver-template-for-master-1 hash: dca0ec96c1010ef7509ea293180e0334
Static pod: kube-apiserver-template-for-master-1 hash: b745f7117ed8859a23a89ae4ef65c7ce
[apiclient] Found 1 Pods for label selector component=kube-apiserver
[upgrade/staticpods] Component "kube-apiserver" upgraded successfully!
[upgrade/staticpods] Preparing for "kube-controller-manager" upgrade
[upgrade/staticpods] Renewing controller-manager.conf certificate
[upgrade/staticpods] Moved new manifest to "/etc/kubernetes/manifests/kube-controller-manager.yaml" and backed up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2021-03-23-18-04-09/kube-controller-manager.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This might take a minute or longer depending on the component/version gap (timeout 5m0s)
Static pod: kube-controller-manager-template-for-master-1 hash: c43b349fe40aab07b8e29b4a2be8c4af
Static pod: kube-controller-manager-template-for-master-1 hash: d2348e74203d3930979c00d811721b6c
[apiclient] Found 1 Pods for label selector component=kube-controller-manager
[upgrade/staticpods] Component "kube-controller-manager" upgraded successfully!
[upgrade/staticpods] Preparing for "kube-scheduler" upgrade
[upgrade/staticpods] Renewing scheduler.conf certificate
[upgrade/staticpods] Moved new manifest to "/etc/kubernetes/manifests/kube-scheduler.yaml" and backed up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2021-03-23-18-04-09/kube-scheduler.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This might take a minute or longer depending on the component/version gap (timeout 5m0s)
Static pod: kube-scheduler-template-for-master-1 hash: d2768f36096b01759dbdef9ca638ffd0
Static pod: kube-scheduler-template-for-master-1 hash: 5795d0c442cb997ff93c49feeb9f6386
[apiclient] Found 1 Pods for label selector component=kube-scheduler
[upgrade/staticpods] Component "kube-scheduler" upgraded successfully!
[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config-1.18" in namespace kube-system with the configuration for the kubelets in the cluster
[kubelet-start] Downloading configuration for the kubelet from the "kubelet-config-1.18" ConfigMap in the kube-system namespace
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstrap-token] configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstrap-token] configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

[upgrade/successful] SUCCESS! Your cluster was upgraded to "v1.18.0". Enjoy!
```
```
root@template-for-master-1:~# kubeadm version
kubeadm version: &version.Info{Major:"1", Minor:"18", GitVersion:"v1.18.0", GitCommit:"9e991415386e4cf155a24b1da15becaa390438d8", GitTreeState:"clean", BuildDate:"2020-03-25T14:56:30Z", GoVersion:"go1.13.8", Compiler:"gc", Platform:"linux/amd64"}

root@template-for-master-1:~# kubectl describe pod kube-apiserver-template-for-master-1 -n kube-system
Name:                 kube-apiserver-template-for-master-1
Namespace:            kube-system
Priority:             2000000000
Priority Class Name:  system-cluster-critical
Node:                 template-for-master-1/10.166.0.31
Start Time:           Tue, 23 Mar 2021 18:00:48 +0000
Labels:               component=kube-apiserver
                      tier=control-plane
Annotations:          kubeadm.kubernetes.io/kube-apiserver.advertise-address.endpoint: 10.166.0.31:6443
                      kubernetes.io/config.hash: b745f7117ed8859a23a89ae4ef65c7ce
                      kubernetes.io/config.mirror: b745f7117ed8859a23a89ae4ef65c7ce
                      kubernetes.io/config.seen: 2021-03-23T18:04:11.56746527Z
                      kubernetes.io/config.source: file
Status:               Running
IP:                   10.166.0.31
IPs:
  IP:           10.166.0.31
Controlled By:  Node/template-for-master-1
Containers:
  kube-apiserver:
    Container ID:  docker://c97d0ffd48463a05fb9b8796e64b4949d646b5d693f4d028274950b3b4f7d267
    Image:         k8s.gcr.io/kube-apiserver:v1.18.0
    Image ID:      docker-pullable://k8s.gcr.io/kube-apiserver@sha256:fc4efb55c2a7d4e7b9a858c67e24f00e739df4ef5082500c2b60ea0903f18248
    Port:          <none>
    Host Port:     <none>
    Command:
      kube-apiserver
      --advertise-address=10.166.0.31
      --allow-privileged=true
      --authorization-mode=Node,RBAC
      --client-ca-file=/etc/kubernetes/pki/ca.crt
      --enable-admission-plugins=NodeRestriction
      --enable-bootstrap-token-auth=true
      --etcd-cafile=/etc/kubernetes/pki/etcd/ca.crt
      --etcd-certfile=/etc/kubernetes/pki/apiserver-etcd-client.crt
      --etcd-keyfile=/etc/kubernetes/pki/apiserver-etcd-client.key
      --etcd-servers=https://127.0.0.1:2379
      --insecure-port=0
      --kubelet-client-certificate=/etc/kubernetes/pki/apiserver-kubelet-client.crt
      --kubelet-client-key=/etc/kubernetes/pki/apiserver-kubelet-client.key
      --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname
      --proxy-client-cert-file=/etc/kubernetes/pki/front-proxy-client.crt
      --proxy-client-key-file=/etc/kubernetes/pki/front-proxy-client.key
      --requestheader-allowed-names=front-proxy-client
      --requestheader-client-ca-file=/etc/kubernetes/pki/front-proxy-ca.crt
      --requestheader-extra-headers-prefix=X-Remote-Extra-
      --requestheader-group-headers=X-Remote-Group
      --requestheader-username-headers=X-Remote-User
      --secure-port=6443
      --service-account-key-file=/etc/kubernetes/pki/sa.pub
      --service-cluster-ip-range=10.96.0.0/12
      --tls-cert-file=/etc/kubernetes/pki/apiserver.crt
      --tls-private-key-file=/etc/kubernetes/pki/apiserver.key
    State:          Running
      Started:      Tue, 23 Mar 2021 18:04:12 +0000
    Ready:          True
    Restart Count:  0
    Requests:
      cpu:        250m
    Liveness:     http-get https://10.166.0.31:6443/healthz delay=15s timeout=15s period=10s #success=1 #failure=8
    Environment:  <none>
    Mounts:
      /etc/ca-certificates from etc-ca-certificates (ro)
      /etc/kubernetes/pki from k8s-certs (ro)
      /etc/ssl/certs from ca-certs (ro)
      /usr/local/share/ca-certificates from usr-local-share-ca-certificates (ro)
      /usr/share/ca-certificates from usr-share-ca-certificates (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  ca-certs:
    Type:          HostPath (bare host directory volume)
    Path:          /etc/ssl/certs
    HostPathType:  DirectoryOrCreate
  etc-ca-certificates:
    Type:          HostPath (bare host directory volume)
    Path:          /etc/ca-certificates
    HostPathType:  DirectoryOrCreate
  k8s-certs:
    Type:          HostPath (bare host directory volume)
    Path:          /etc/kubernetes/pki
    HostPathType:  DirectoryOrCreate
  usr-local-share-ca-certificates:
    Type:          HostPath (bare host directory volume)
    Path:          /usr/local/share/ca-certificates
    HostPathType:  DirectoryOrCreate
  usr-share-ca-certificates:
    Type:          HostPath (bare host directory volume)
    Path:          /usr/share/ca-certificates
    HostPathType:  DirectoryOrCreate
QoS Class:         Burstable
Node-Selectors:    <none>
Tolerations:       :NoExecute
Events:
  Type    Reason   Age    From                            Message
  ----    ------   ----   ----                            -------
  Normal  Pulled   4m20s  kubelet, template-for-master-1  Container image "k8s.gcr.io/kube-apiserver:v1.18.0" already present on machine
  Normal  Created  4m20s  kubelet, template-for-master-1  Created container kube-apiserver
  Normal  Started  4m20s  kubelet, template-for-master-1  Started container kube-apiserver
```

- [V] Выведем ноду из эксплуатации:
```
root@template-for-master-1:~# kubectl get nodes -o wide
NAME                    STATUS                     ROLES    AGE   VERSION   INTERNAL-IP   EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION   CONTAINER-RUNTIME
template-for-master-1   Ready                      master   34m   v1.18.0   10.166.0.31   <none>        Ubuntu 18.04.5 LTS   5.4.0-1038-gcp   docker://19.3.8
template-for-worker-1   Ready,SchedulingDisabled   <none>   19m   v1.17.4   10.166.0.32   <none>        Ubuntu 18.04.5 LTS   5.4.0-1038-gcp   docker://19.3.8
template-for-worker-2   Ready                      <none>   19m   v1.17.4   10.166.0.33   <none>        Ubuntu 18.04.5 LTS   5.4.0-1038-gcp   docker://19.3.8
template-for-worker-3   Ready                      <none>   19m   v1.17.4   10.166.0.34   <none>        Ubuntu 18.04.5 LTS   5.4.0-1038-gcp   docker://19.3.8
```
- [V] Обновил воркер ноду :
```
root@template-for-master-1:~# kubectl get nodes
NAME                    STATUS                     ROLES    AGE   VERSION
template-for-master-1   Ready                      master   36m   v1.18.0
template-for-worker-1   Ready,SchedulingDisabled   <none>   21m   v1.18.0
template-for-worker-2   Ready                      <none>   21m   v1.17.4
template-for-worker-3   Ready                      <none>   21m   v1.17.4
```
- [V] Обновил оставшиеся ноды :
```
root@template-for-master-1:~# kubectl get nodes
NAME                    STATUS   ROLES    AGE   VERSION
template-for-master-1   Ready    master   39m   v1.18.0
template-for-worker-1   Ready    <none>   25m   v1.18.0
template-for-worker-2   Ready    <none>   24m   v1.18.0
template-for-worker-3   Ready    <none>   24m   v1.18.0
```

- [V] Установил с помощью kubespray:
```
PLAY RECAP *****************************************************************************************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node1                      : ok=532  changed=107  unreachable=0    failed=0    skipped=633  rescued=0    ignored=1
node2                      : ok=345  changed=67   unreachable=0    failed=1    skipped=394  rescued=0    ignored=1
node3                      : ok=345  changed=67   unreachable=0    failed=1    skipped=393  rescued=0    ignored=1
node4                      : ok=345  changed=67   unreachable=0    failed=1    skipped=393  rescued=0    ignored=1

Tuesday 23 March 2021  22:16:19 +0300 (0:00:00.425)       0:08:06.681 *********
===============================================================================
container-engine/docker : ensure docker packages are installed ----------------------------------------------------------------------------- 28.67s
kubernetes/control-plane : kubeadm | Initialize first master ------------------------------------------------------------------------------- 17.95s
wait for etcd up --------------------------------------------------------------------------------------------------------------------------- 10.18s
kubernetes/preinstall : Install packages requirements --------------------------------------------------------------------------------------- 9.71s
download_container | Download image if required --------------------------------------------------------------------------------------------- 8.17s
download_container | Download image if required --------------------------------------------------------------------------------------------- 7.30s
kubernetes/preinstall : Update package management cache (APT) ------------------------------------------------------------------------------- 6.29s
download_container | Download image if required --------------------------------------------------------------------------------------------- 5.63s
Configure | Check if etcd cluster is healthy ------------------------------------------------------------------------------------------------ 5.45s
kubernetes/preinstall : Get current calico cluster version ---------------------------------------------------------------------------------- 5.17s
Configure | Wait for etcd cluster to be healthy --------------------------------------------------------------------------------------------- 5.14s
download_file | Download item --------------------------------------------------------------------------------------------------------------- 5.08s
download_container | Download image if required --------------------------------------------------------------------------------------------- 4.41s
download_container | Download image if required --------------------------------------------------------------------------------------------- 4.39s
download : check_pull_required |  Generate a list of information about the images on a node ------------------------------------------------- 4.18s
download_container | Download image if required --------------------------------------------------------------------------------------------- 4.02s
download_container | Download image if required --------------------------------------------------------------------------------------------- 3.84s
download_file | Download item --------------------------------------------------------------------------------------------------------------- 3.74s
download_container | Download image if required --------------------------------------------------------------------------------------------- 3.65s
download_file | Download item --------------------------------------------------------------------------------------------------------------- 3.45s
```
```
root@node1:~# kubectl get nodes
NAME    STATUS   ROLES                  AGE     VERSION
node1   Ready    control-plane,master   2m26s   v1.20.5
node2   Ready    <none>                 2m26s   v1.20.5
node3   Ready    <none>                 2m26s   v1.20.5
node4   Ready    <none>                 2m26s   v1.20.5
```

## PR checklist:
 - [V] Выставлен label с темой домашнего задания
 </details>
