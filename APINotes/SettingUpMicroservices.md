In order to set up a microservice, first create new databases in your local mysql instance.
For instance, if I wanted user-service and uaa-service, I would create sh_user and sh_uaa in mysql:

```bash
mysql -u root p
```
```mysql
CREATE DATABASE sh_user;
CREATE DATABASE sh_uaa;
```

Since the MQ running on fakie does not allow remote access, make sure to install RabbitMQ locally.
You can do so either going to their website and installing it manually, or you can use a package manager (like homebrew for mac).
You can get instructions for either on https://www.rabbitmq.com/download.html

Once done installing homebrew, navigate to /usr/local/sbin and type:

```bash
open rabbitmq-server
```

Before running microservices, make sure to go to their respective application.properties files.
For user microservice, that would be in sh_repo/applications/webApps/microservices/services/user-service/src/main/resources/application.properties
Change the rabbitmq.host to localhost and rabbitmq.port to 5672.
```
rabbitmq.host=localhost
rabbitmq.port=5672
```
You also need to change your spring.datasource.password to your own password.
And finally, change your datasource.url. For my user service application.properties file, I would have:
```
jdbc:mysql://localhost:3306/sh_user?autoReconnect=true&amp;createDatabaseIfNotExist=true&amp;useUnicode=true&amp;characterEncoding=utf-8
```
