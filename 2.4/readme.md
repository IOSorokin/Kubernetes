# Домашнее задание к занятию «Управление доступом»

## Задание 1. Создайте конфигурацию для подключения пользователя

   1. Создайте и подпишите SSL-сертификат для подключения к кластеру.
   2. Настройте конфигурационный файл kubectl для подключения.
   3. Создайте роли и все необходимые настройки для пользователя.
   4. Предусмотрите права пользователя. Пользователь может просматривать логи подов и их конфигурацию (kubectl logs pod <pod_id>, kubectl describe pod <pod_id>).
   5. Предоставьте манифесты и скриншоты и/или вывод необходимых команд.


 _____________________________________________________________________________________________________________________________________________________________________

 1. Создадим конфигурацию для подключения пользователя используя SSL

 ![image](https://github.com/user-attachments/assets/acdec0bf-1773-49ed-815c-abbc0e5a3d9d)

Создам запрос на подписание сертификата (CSR)

![image](https://github.com/user-attachments/assets/8528ed52-e167-4553-a243-451996496e22)

Сгенерирую файл сертификата (CRT). Поскольку я использую Microk8s, я буду использовать ключи кластера по пути /var/snap/microk8s/current/certs/

![image](https://github.com/user-attachments/assets/54ca60bc-0a9d-46c6-b3b1-a42d30cdfd64)

2. Настрою конфигурационный файл kubectl для подключения.

Создам пользователя staff и настраиваю его на использование созданного выше ключа

![image](https://github.com/user-attachments/assets/ae077e93-9a0f-4069-9073-86ac13102e71)

Создам новый контекст с именем staff-context и подключу его к пользователю staff, созданному ранее

![image](https://github.com/user-attachments/assets/abea9bc9-93b3-487c-b3a0-c4157bdaafce)

Проверим создался ли контест

![image](https://github.com/user-attachments/assets/442882dd-26f5-4b4a-baa9-b080fc29f9fb)

Видим что контекст создался

3. Создадим новый namespace

![image](https://github.com/user-attachments/assets/866c87ca-e296-4659-819b-77ee069ed0ce)

Еще потребуется включение встроенного в Microk8s RBAC контроллера

![image](https://github.com/user-attachments/assets/dfd7fe79-fe04-40a9-aa00-f4c2accf9176)

Применим манифесты role и rolebinding и проверяю их 

![image](https://github.com/user-attachments/assets/eeb4264d-9c20-4514-80ca-e57e55b2afb6)

4. Для проверки прав пользователя переключусь в его контекст

![image](https://github.com/user-attachments/assets/7ef6d7ce-cbd7-4765-801b-a2cb2bb0a03d)

Развернем Deployment в разрешенном для пользователя Namespace

![image](https://github.com/user-attachments/assets/6fcb7e99-5226-40d7-a7b3-f1c8a2468d92)

Проверим какие развернуты поды в Namespace с именем default

![image](https://github.com/user-attachments/assets/99df5f3a-1785-44af-87b7-eb4a71762d1c)

Видим, что в Namespace с именем default нет доступа, так как он не был указан в манифесте Role.

Но если же мы проверим namespace "access" мы в нем все увидит так, как у нас есть в него доступ

![image](https://github.com/user-attachments/assets/7186f010-2353-4df9-8ab2-6ed5f3095308)

Так же проверим логи пода

![image](https://github.com/user-attachments/assets/52f47d0e-1792-499f-a7ff-1cad9cccd5af)

И проверю вывпод пода

![image](https://github.com/user-attachments/assets/eb624311-10d3-40ee-a1c0-946319634c33)

Согласно манифесту роли и ее привязке к Namespace, у пользователя staff есть доступ подам, их логам и описанию.

5. Ссылки на манифесты:

Ссылка на манифест Deployment: 
Ссылка на манифест Role:
Ссылка на манифест RoleBinding:
