[![Java CI with Maven](https://github.com/evgenkolesman/SimpleChat/actions/workflows/maven.yml/badge.svg)](https://github.com/evgenkolesman/SimpleChat/actions/workflows/maven.yml)

#  SimpleChat

1.     OpenApi доки после запуска приложения тут: 

OpenApi
        <http://localhost:8080/swagger-ui/index.html>

        так же для описания и подделжки добавлен Actuator с дефолтными ендпоинтами, пример: localhost:8080/actuator/info.
2.     Авторизацию реализовал чисто символическую, так как для это го нужен фактически еще сервис,
       у нас при входе отпраляется POST запрос на /api/v1/auth если все ок то через kafka передается "токен",
       конечно лучше было бы реализовать через OAuth 2 – но пока не хватило времени. 
-      Начал подключать OAuth 2, есть проблемы с тестированием все пока убрал, так как понадобиться подключать для тестирования доп клиент
       для получения токена. 
       Проблема, необходимая для решения, это создать клиента (применяем OpenFeign или RestTemplate) для тестового профиля, 
       и с помощью него каждый раз получать токен авторизации (возможно в дальнейшем будет решена)

3.     В остальном просто REST приложение с 3-мя сервисами: Авторизация, Работа с сообщениями, Работа с пользователями.
-      Тестирование осуществляется с помощью TestContainers и RestAssured, Docker-compose можно развернуть код ниже.
       там хранятся контейнеры для локальной работы, возможно добавлю еще имадж самого приложения и будет все вместе подниматься;

Чтобы запустить приложение необходимо его скопировать: 
-      git clone https://github.com/evgenkolesman/SimpleChat
запустить инвайрмент вместе с приложением 
-      docker-compose up

далее можно поднять только необходимые контейнеры для работы приложения (из докер компоуза) и сделать команду
-      mvn spring-boot:run 

или 
-      mvn org.springframework.boot:spring-boot-maven-plugin:run

если проблемы с Maven:
-      java -jar target/simplechat-0.0.1-SNAPSHOT.jar

ну или ручками в идее запустить

PS: если есть проблемы с портами в линухе, пример:

Проблема с портом 5432:

`fuser -vn tcp 5432`
получаем номер процесса, например `11111`

`kill 11111` - убиваем процесс
