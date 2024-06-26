# Домашнее задание к занятию «Сетевое взаимодействие в K8S. Часть 1»

## Задание 1. Создать Deployment и обеспечить доступ к контейнерам приложения по разным портам из другого Pod внутри кластера

### 1. Создать Deployment приложения, состоящего из двух контейнеров (nginx и multitool), с количеством реплик 3 шт.
  Сначала удаляю namespace с предыдущего задания и добавлю namespace с именем "netology-net" для текущего домашнего задания

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/a039b553-023c-4fac-9278-e65f503b0c2a)

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/b8e1788a-4281-4205-96d5-84c78434d98a)

Создал манифест, состоящего из двух контейнеров (nginx и multitool), с количеством реплик 3 шт.

Видим что создано 3 реплики

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/db298b54-1d0a-436b-b7e3-a2049cad9927)

### 2. Создать Service, который обеспечит доступ внутри кластера до контейнеров приложения из п.1 по порту 9001 — nginx 80, по 9002 — multitool 8080.

Создал манифест для service настроил доступ по портам 9001 и 9002 как указано в задании
Ссылка на манифест:

Применяю его 

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/6dca5192-5995-44bb-a227-7a1d43b74df5)

Вижу , что сервис создан и слушает порты 9001 и 9002


### 3. Создать отдельный Pod с приложением multitool и убедиться с помощью curl, что из пода есть доступ до приложения из п.1 по разным портам в разные контейнеры.

Пишу манифест отдельного Pod, с приложением multitool и запускаю его:
Ссылка на манифест:

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/b83977e9-69ec-450d-a410-8d9553e41c80)

Вижу, что он создан успешно 

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/18be014f-1c86-4d59-aeb3-19bb7fe738eb)

### 4. Продемонстрировать доступ с помощью curl по доменному имени сервиса.

Из пода multitool проверяю доступность приложений в подах по одному из IP адресов:

Вхожу в pod multitool

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/a596f20b-7fc3-4cd6-b844-dd4e1a27ef74)

Проверяю доступность приложений 

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/02d1f817-c71e-4d59-939d-b43d3e425e44)

Проложения доступны

Проверяю сервисы по доменному имени

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/c4018759-7bf3-4428-9da3-7d3a17dcf220)

Ответил NGINX по порту 9001

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/7b3c7905-a79d-4ab5-86ac-f6641ca5daab)

Ответил Multitool по порту 9002

### 5. Предоставить манифесты Deployment и Service в решении, а также скриншоты или вывод команды п.4.
Ссылка на манифест Deployments: https://github.com/IOSorokin/Kubernetes/blob/main/1.4/YAML/deployment.yaml 

Ссылка на манифест Service: https://github.com/IOSorokin/Kubernetes/blob/main/1.4/YAML/service.yaml

Ссылка на манифест Pod multitool: https://github.com/IOSorokin/Kubernetes/blob/main/1.4/YAML/multitool.yaml



## Задание 2. Создать Service и обеспечить доступ к приложениям снаружи кластера

###  Создать отдельный Service приложения из Задания 1 с возможностью доступа снаружи кластера к nginx, используя тип NodePort.

Создал отдельный Service приложения из Задания 1 с возможностью доступа снаружи кластера к nginx, используя тип NodePort

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/472c9e12-3e62-4b97-8c4b-f7f79e234df1)


### Продемонстрировать доступ с помощью браузера или curl с локального компьютера.

Предоставляю вывод curl
![изображение](https://github.com/IOSorokin/Kubernetes/assets/148979909/c4d49894-b631-4bcf-8a96-b25f694bf348)
Видим что pod доступен по порту 30000

Проверяем доступность multitool

![изображение](https://github.com/IOSorokin/Kubernetes/assets/148979909/dede0428-6d2d-4257-94c4-b4bb02f2eeb5)

Он тоже доступен по порту 30001

### Предоставить манифест и Service в решении, а также скриншоты или вывод команды п.2.
Ссылка на манифест NodePort: https://github.com/IOSorokin/Kubernetes/blob/main/1.4/YAML/svc-nodeport.yaml

