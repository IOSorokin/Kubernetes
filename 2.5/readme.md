# Домашнее задание к занятию «Helm»

## Задание 1. Подготовить Helm-чарт для приложения

Установлю на ноду Helm используя скрипт:

![image](https://github.com/user-attachments/assets/d683095f-78d7-4931-b73c-063ffb66fcc9)

Создаю собственный helm chart с именем myhelm-grafana:

![image](https://github.com/user-attachments/assets/d154b0ff-5fba-48cd-b24e-d243dd0a2f00)

Создаю два файла Values - values_dvl.yaml и values_test.yaml для DEVELOP и TEST окружения. 
И дописываю в них необходимые параметры для запуска Grafana, такие как имя образа, тег, порт. Приложения будут развернуты отдельными Deployment.

## Задание 2. Запустить две версии в разных неймспейсах

Создам отдельный Namespace с именем app1, запущу обе версии приложения в этом Namespace:

![image](https://github.com/user-attachments/assets/7da3cc79-9732-432b-baa4-46328d23f9d3)

![image](https://github.com/user-attachments/assets/8671937b-3949-4cd2-8595-87ede1956761)

Проверю результат

![image](https://github.com/user-attachments/assets/afdec573-e8cd-4f37-8163-b38b6f50262b)

Все создалось

Разверну еще одну версию приложения, но уже в Namespace app2

![image](https://github.com/user-attachments/assets/fc7d04bd-e593-461c-bdd0-a1092d144134)

Приложение так же успешно развернуто. 

Проверю откроется ли Web-интерфейс приложения:

![image](https://github.com/user-attachments/assets/41178bc4-52e4-4e36-8c18-016451668fb7)

Видем, что запустилась вресия графана которая описана в файле переменных values_preprod.yaml тегу main.

