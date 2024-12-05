# Домашнее задание к занятию «Управление доступом» Шарапат Виктор

### Цель задания

В тестовой среде Kubernetes нужно предоставить ограниченный доступ пользователю.

------

### Чеклист готовности к домашнему заданию

1. Установлено k8s-решение, например MicroK8S.
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключённым github-репозиторием.

------

### Инструменты / дополнительные материалы, которые пригодятся для выполнения задания

1. [Описание](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) RBAC.
2. [Пользователи и авторизация RBAC в Kubernetes](https://habr.com/ru/company/flant/blog/470503/).
3. [RBAC with Kubernetes in Minikube](https://medium.com/@HoussemDellai/rbac-with-kubernetes-in-minikube-4deed658ea7b).

------

### Задание 1. Создайте конфигурацию для подключения пользователя

1. Создайте и подпишите SSL-сертификат для подключения к кластеру.
2. Настройте конфигурационный файл kubectl для подключения.
3. Создайте роли и все необходимые настройки для пользователя.
4. Предусмотрите права пользователя. Пользователь может просматривать логи подов и их конфигурацию (`kubectl logs pod <pod_id>`, `kubectl describe pod <pod_id>`).
5. Предоставьте манифесты и скриншоты и/или вывод необходимых команд.

------

### Правила приёма работы

1. Домашняя работа оформляется в своём Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl`, скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.

------

### Решение 1

На машине кубера

* Создайте ключ для пользователя:

[image](https://github.com/user-attachments/assets/34a4b799-1d1d-4716-a65b-dbf09def19d2)

* Создайте запрос на подпись сертификата (CSR):

![image](https://github.com/user-attachments/assets/09734093-d9a2-4179-9e9e-808007d7463d)

* Подпишите CSR с использованием CA кластера:

## openssl x509 -req -in admon.csr -CA /var/snap/microk8s/current/certs/ca.crt -CAkey /var/snap/microk8s/current/certs/ca.key -CAcreateserial -out admon.crt -days 365

![image](https://github.com/user-attachments/assets/7073caeb-7657-440c-b5c1-ff72c4a20e2f)

* Создайте роль с правами на просмотр логов и описания подов:

![image](https://github.com/user-attachments/assets/40bff339-d31c-4f2e-a2e6-edad5f950d30)

* Примените привязку:

![image](https://github.com/user-attachments/assets/ea84717a-c985-463e-a417-3ad9b264b18f)


На узле с kubectl (192.168.2.223)

* Скопировал файлы admon.crt, admon.key и ca.crt с узла MicroK8S на узел kubectl

* Создайте конфигурационный файл для пользователя:

![image](https://github.com/user-attachments/assets/79e05edd-8c11-49b0-8bc0-83fe05bd8895)

* Проверьте конфигурацию:

![image](https://github.com/user-attachments/assets/fe31c524-34b8-4105-97b2-60875e91413a)





 


  

---

