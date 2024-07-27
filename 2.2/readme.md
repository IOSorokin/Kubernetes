# Домашнее задание к занятию «Хранение в K8s. Часть 2»

## Задание 1

Что нужно сделать

Создать Deployment приложения, использующего локальный PV, созданный вручную.

  ###  Создать Deployment приложения, состоящего из контейнеров busybox и multitool.

Создал deployment приложения состоящего из busybox и multitool. Применяю его и проверяю статус

![изображение](https://github.com/IOSorokin/Kubernetes/assets/148979909/6f7f0c89-bff9-4890-ba0c-be19b74fd14b)

все создалось успешно, но статус pod PENDING это связано с тем, что отсутствует PVC с именем pvc-vol.
  
  ###  Создать PV и PVC для подключения папки на локальной ноде, которая будет использована в поде.
  
Создам манифест для создания PV и PVC для подключения папки на локальной ноде, которая будет использована в поде.

Применяю манифесты и проверяю статус

![изображение](https://github.com/IOSorokin/Kubernetes/assets/148979909/fb6a27b1-deac-4f82-ae92-7262684bbd25)

PV и PVC запущены.

Теперь проверю статус пода, который ожидал создания PVC с именем pvc-vol:

![изображение](https://github.com/user-attachments/assets/e4410b95-f445-4cdf-9654-84151ceabd85)

Под запущен

  ###  Продемонстрировать, что multitool может читать файл, в который busybox пишет каждые пять секунд в общей директории.

Проверю, сможет ли multitool прочитать файл, в который busybox пишет данные каждые пять секунд в общей директории.

Проверить доступность файла можно из самого контейнера:

![изображение](https://github.com/user-attachments/assets/c0a6818f-a01f-48df-9424-269b1998973c)

Также можно посмотреть логи самого контейнера в поде:

![изображение](https://github.com/user-attachments/assets/7e02f2e8-280f-4b55-9f1c-36b1224efa7c)

Multitool имеет досуп к файлу и может прочесть его. 
  
  ###  Удалить Deployment и PVC. Продемонстрировать, что после этого произошло с PV. Пояснить, почему.

Удаляю Deployment и PVC:

![изображение](https://github.com/user-attachments/assets/d44ce108-d53b-415f-a250-07344a79bb80)

Проверю что произошло после этого с PV

![изображение](https://github.com/user-attachments/assets/6b6df3d0-a43d-4ffe-912f-ab7806219b6d)

PV перешел в состояние failed так как контроллер PV не сумел удалить данные по пути /data/pvc-first. По умолчанию он может удалить только данные по пути /tmp. Если бы там находились файлы, то они были бы утеряны.

  ###  Продемонстрировать, что файл сохранился на локальном диске ноды. Удалить PV. Продемонстрировать что произошло с файлом после удаления PV. Пояснить, почему.

Если же PVC не удалять, а удалить только Deployment, то PV будет в статусе "Bound"

![изображение](https://github.com/user-attachments/assets/1883c1f9-1a54-4ee8-9d89-4412ce76e0b4)

Проверю сохранился ли файл на диске

![изображение](https://github.com/user-attachments/assets/82cbcc17-f3e1-4ecf-b70b-5a4d60630950)

Файл присутствует...

  
  ###  Предоставить манифесты, а также скриншоты или вывод необходимых команд.

Ссылка на deployment: https://github.com/IOSorokin/Kubernetes/blob/main/2.2/YAML/deployment.yaml

Ссылка на PV: https://github.com/IOSorokin/Kubernetes/blob/main/2.2/YAML/pv.yaml

Ссылка на PVC: https://github.com/IOSorokin/Kubernetes/blob/main/2.2/YAML/pvc.yaml


## Задание 2

Что нужно сделать

Создать Deployment приложения, которое может хранить файлы на NFS с динамическим созданием PV.

   ### Включить и настроить NFS-сервер на MicroK8S.
   
  Устанавливаю и настраиваю NFS-сервер на ноде с MicroK8S

![изображение](https://github.com/user-attachments/assets/5274d01c-5654-4eff-a62e-5bc5e6b785e7)


   ### Создать Deployment приложения состоящего из multitool, и подключить к нему PV, созданный автоматически на сервере NFS.

  Создаю манифест deployment_nfs и применяю его. 

![изображение](https://github.com/user-attachments/assets/57b1ad58-a300-4136-817c-5a755bb40292)

  Так как в манифесте я указал использование NFS сервера, но еще не создал PVC, поэтому под будет находиться в режиме ожидания.

Проверяю PV вижу что он создался автоматически

![изображение](https://github.com/user-attachments/assets/5a41b11f-dddb-4d0b-9efe-02d068052edc)

Пишу и запускаю манифест PVC, а также посмотрю состояние пода:

![изображение](https://github.com/user-attachments/assets/227c9f56-07c9-4d8d-882d-5bcfe2f67455)


При появлении PVC с именем, указанным в манифесте Deployment, под запускается и переходит в режим готовности.

   ### Продемонстрировать возможность чтения и записи файла изнутри пода.

Проверяю возможность чтения и записи файла изнутри пода.

![изображение](https://github.com/user-attachments/assets/3200060b-5b73-45cb-8599-c9f6081706c0)

Вижу что файл создан успешно
   
   ### Предоставить манифесты, а также скриншоты или вывод необходимых команд.

Манифест deployment_nfs  : https://github.com/IOSorokin/Kubernetes/blob/main/2.2/YAML/deployment_nfs.yaml
Манифест pvc_nfs    : https://github.com/IOSorokin/Kubernetes/blob/main/2.2/YAML/pvc_nfs.yaml
