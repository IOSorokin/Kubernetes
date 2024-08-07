# Домашнее задание к занятию «Сетевое взаимодействие в K8S. Часть 2»

## Задание 1. Создать Deployment приложений backend и frontend

 ### 1.  Создать Deployment приложения frontend из образа nginx с количеством реплик 3 шт.

Создал Deployment для приложения frontend с тремя репликами в новом namespace "netology-net-2"

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/fbf8b80c-6f15-4d12-b191-8beb962257b5)

Ссылка на манифест: Frontend:

 ###  2.  Создать Deployment приложения backend из образа multitool.

Создал Deployment для приложения Backend из образа multitool

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/51697a1c-8add-46dc-9454-d7ca7670a6a4)

Ссылка на манифест Backend:

Проверяем все ли доступно и создалось, видно что все поды создались

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/7155ad29-da26-43fa-85c4-f67e01e13d99)



 ### 3.  Добавить Service, которые обеспечат доступ к обоим приложениям внутри кластера.

Создал манифест Service для обеспечения доступа к обоим приложениям

Проверяю все ли создалось: 

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/0ce375f6-988b-497a-b5e3-17f5ac133136)

Все создалось успешно

Ссылка на манифест Service:

  
 ### 4.  Продемонстрировать, что приложения видят друг друга с помощью Service.

Используя curl проверяю, видят ли приложения друг-друга

Из под backend доступность есть

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/2a526d5d-05cd-46a9-acf6-6f0ca42e9724)

Из под front тоже вижу доступность

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/c1dd7feb-d9e8-4ae1-b165-bd667f23af71)


 
 ### 5.  Предоставить манифесты Deployment и Service в решении, а также скриншоты или вывод команды п.4.

Манифест Frontend: https://github.com/IOSorokin/Kubernetes/blob/main/1.5/YAML/front_deploy.yaml

Манифест Backend: https://github.com/IOSorokin/Kubernetes/blob/main/1.5/YAML/back_deploy.yaml

Манифест Service: https://github.com/IOSorokin/Kubernetes/blob/main/1.5/YAML/service.yaml

## Задание 2. Создать Ingress и обеспечить доступ к приложениям снаружи кластера

 ### 1.  Включить Ingress-controller в MicroK8S.

Включил Ingress-controller в MicroK8S, проверил его работоспособность:

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/faeef2e7-6a43-4494-ae20-6eab04e1724d)

Проверяю его доступность:

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/2fe244b9-8c6c-4a16-8c86-c61d07ab0293)

 
 ### 2.  Создать Ingress, обеспечивающий доступ снаружи по IP-адресу кластера MicroK8S так, чтобы при запросе только по адресу открывался frontend а при добавлении /api - backend.

Пишу манифест ingress обеспеивающий доступ снаружи по IP-адреса кластера MikroK8S, применяю его:

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/6297d391-e13c-4ddc-8709-4c011ceb8bf3)

Вижу что ingress создан
 
 ### 3.  Продемонстрировать доступ с помощью браузера или curl с локального компьютера.

Для того, чтобы можно было попасть на под через curl с локального комьютера, нужно прописать имя сайта в файле hosts. Чтобы http://netologyingress.com ссылался на localhost.
Проверяем после добавления.

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/1a9154ef-f3ff-4954-aff5-c5c1da883ed5)


При обращении на http://netologyingress.com вижу, что отвечает NGINX, а при обращении на http://netologyingress.com/api отвечает multitool. Отсюда вывод, что все поднялось и работает корректно.
 
 ### 4.  Предоставить манифесты и скриншоты или вывод команды п.2.
 
Манифест Ingress: https://github.com/IOSorokin/Kubernetes/blob/main/1.5/YAML/ingress.yaml
