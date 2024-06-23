# Домашнее задание к занятию «Запуск приложений в K8S»

## Цель задания

В тестовой среде для работы с Kubernetes, установленной в предыдущем ДЗ, необходимо развернуть Deployment с приложением, состоящим из нескольких контейнеров, и масштабировать его.
Чеклист готовности к домашнему заданию

    Установленное k8s-решение (например, MicroK8S).
    Установленный локальный kubectl.
    Редактор YAML-файлов с подключённым git-репозиторием.

# Задание 1. Создать Deployment и обеспечить доступ к репликам приложения из другого Pod

## Для начала создаю отдельный Namespace где буду разворачивать приложение и проверяю что он создался
![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/7f465029-1827-4a3b-a45e-57b726ec446c)

##    Создать Deployment приложения, состоящего из двух контейнеров — nginx и multitool. Решить возникшую ошибку.
  Создал манифест для двух приложений. Так как у меня запущен Ingress с nginx в поде nginx-ingress-microk8s-controller-tdkdf, то порты 80, 443 будут заняты. Когда эти порты заняты, запуск multitool потребует указания альтернативного порта. Для этого в манифест Deployment добавляю переменную с указанием порта 1180.
Пример файла deployment.yaml доступен по ссылке:

Запускаю его и проверяю результат

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/4c42b8a1-39d6-43f6-93dc-154aac26b421)

Из срина выше видно что запущена одна реплика приложения nginx-multitool. Увеличу количество реплик до двух и проверю результат:

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/65c67359-d6c8-485a-aad3-9f6b92a2bcca)

Пишу манифест service с именем nginx-multitool-svc в namespace netology. Применяю манифест:

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/8dc3cfac-b7a7-4aae-a047-a2e936398c5a)

Проверяю сервисы в namespace netology:

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/7aa93874-80da-46b8-bcd8-8b55cfd983f8)

Сервис создан

Пишу манифест для отдельного пода multitool в namespace netology. Применяю манифест:
Ссылка на манифест:

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/614f6c15-587e-4642-9312-b6f27d557876)

При проверке видно что он создан и запущен

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/e6ad6386-3bcc-41dd-8ad5-3c590a51f968)

Проверяю есть ли из пода multitool доступ до приложений созданных выше

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/e89cfde3-b518-495e-98c5-befc5897b002)

Из скриншота видно что при обращении по порту 80 ответил NGINX

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/070d66eb-a46d-4790-a451-150d8028eb1d)

При обращении по порту 8080 ответил созданный multitool


# Задание 2. Создать Deployment и обеспечить старт основного контейнера при выполнении условий


Создаю манифест Deployment приложения nginx, который запустится только после запуска сервиса. В качестве Init-контейнера использую busybox:
Ссылка на манифест: 

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/5c968c79-8786-45e5-8536-646a454c2b94)


Deployment создан проверю запущен ли он

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/c0ee1523-19a4-49c5-b3e4-db6847c8c8e8)

Видно что он не запущен и находится в состоянии Init:0/1

Создаю манифест Service, применяю его и проверяю запустился ли pod NGINX:
Ссылка на манифест:

![image](https://github.com/IOSorokin/Kubernetes/assets/148979909/a56f4792-c46a-4868-8dc5-a146960aa949)

После запуска сервис, pod NGINX запустился. 
