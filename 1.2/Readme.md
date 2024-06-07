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


Задание 2. Создать Service и подключить его к Pod

    Создать Pod с именем netology-web.
    Использовать image — gcr.io/kubernetes-e2e-test-images/echoserver:2.2.
    Создать Service с именем netology-svc и подключить к netology-web.
    Подключиться локально к Service с помощью kubectl port-forward и вывести значение (curl или в браузере).
