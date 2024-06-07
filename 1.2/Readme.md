# Задание 1. Создать Pod с именем hello-world

   ## Создать манифест (yaml-конфигурацию) Pod.
Создал манифест Pod
  ![изображение](https://github.com/IOSorokin/Kubernetes/assets/148979909/c7c6b95e-510f-45d4-80d8-b4c21dacb322)
    
   ##  Использовать image - gcr.io/kubernetes-e2e-test-images/echoserver:2.2.
Запустил манифест командой: kubectl apply -f echoserver.yaml
   ## Подключиться локально к Pod с помощью kubectl port-forward и вывести значение (curl или в браузере).
Выполнил port-forward
![изображение](https://github.com/IOSorokin/Kubernetes/assets/148979909/3355cd6c-4935-4ac8-8bff-76128eb9d4a1)


Проверил локально 
![изображение](https://github.com/IOSorokin/Kubernetes/assets/148979909/18f4e6ca-0762-4d1e-9a24-b024fde0bd0e)


# Задание 2. Создать Service и подключить его к Pod

   ## Создать Pod с именем netology-web.
   ## Использовать image — gcr.io/kubernetes-e2e-test-images/echoserver:2.2.
   ## Создать Service с именем netology-svc и подключить к netology-web.
Создал манифест с service и pod 
   ![изображение](https://github.com/IOSorokin/Kubernetes/assets/148979909/e2160267-fdbb-4476-b0b9-2d1adf67a5bc)

   ## Подключиться локально к Service с помощью kubectl port-forward и вывести значение (curl или в браузере).
Выполнил манифест и port-forward
![изображение](https://github.com/IOSorokin/Kubernetes/assets/148979909/21227b60-f26d-4e6e-baa8-1c891ad45cfc)

Проверил в браузере
![изображение](https://github.com/IOSorokin/Kubernetes/assets/148979909/f1447f55-3c05-4ece-a4e5-0fbcf97fb860)


Как видем при обращении к сервису netolgy-svc по проброшенному порту 8085 видем ответ от пода netology-web, связь пода с сервисом работает.
