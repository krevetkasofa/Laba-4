## Лабораторная работа 2

**

1. Перед выполнением лабораторной работы номер 4 я установила Docker
2. Далее я написала Dockerfile, для этого я создала пустой текстовый документ с соответствующим названием, в нем я прописала следующие строчки кода:
```bash
FROM ubuntu:latest
RUN apt-get update && apt-get install -y libaa-bin  iputils-ping
```
где **первая строчка** означает, что мой образ будет работать на основе Ubuntu последней доступной версии (latest);
**вторая строчка** указывает, что мы обновляем пакетный менеджер и устанавливаем библиотеку libaa-bin в которой содержится aafire. В образе помимо aafire устанавливаю пакет с утилитой ping

3. Dockerfile готов, закрываю и сохраняю его под этим названием. В терминале в папке с этим файлом запускаю команду сборки образа с тегом “aafire”
```bash
docker build -t aafire .
```
4. Далее запускаю контейнер на основе созданного образа и подключаюсь к нему напрямую. При создании контейнера передаю ему запуск приложения “aafire”, которое находится в папке /usr/bin/aafire
```bash
docker run -it aafire /usr/bin/aafire
```
где -it флажок, который обозначает, что приложение будет работать бесконечно

**Получаем:**
![photo_5361786582362876132_y](https://github.com/user-attachments/assets/e06dee24-56b2-4598-bcac-790a7b938c34)

5. В первом терминале я создала и запустила первый контейнер
```bash
docker run -it --name container_first --network myNetwork aafire:latest
```
6. Затем проделала все то же самое во втором окне терминале для второго контейнера
 ```bash
docker run -it --name container_second --network myNetwork aafire:latest
```
![2-fires](https://github.com/user-attachments/assets/69a33c41-cdba-46da-9847-b5c9c062d5ac)
7. Итого я запустила два контейнера с aafire и оставила их в работающем состоянии.
Открыла ещё одно окно терминала и создала сеть при помощи команды 
 ```bash
docker network create myNetwork 
 ```
8. С помощью команды docker ps я увидела названия контейнеров
![names (1) (2)](https://github.com/user-attachments/assets/2811dcfd-d36f-4471-b4df-3b6093bee955)


9. Я подключила контейнеры к своей сети с помощью команд docker network connect myNetwork .... и docker network connect myNetwork .....

10. Я протестировала соединение между контейнерами утилитой ping

![ping-ping](https://github.com/user-attachments/assets/a3c7d7f1-48a7-4294-a7ae-a8c1ffa66074)

**ИТого:**
Все пингуется, следовательно, контейнеры подключены между собой
