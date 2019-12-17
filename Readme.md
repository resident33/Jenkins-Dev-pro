# **CI/CD**
### **Task:**
Подготовить Jenkinsfile и опубликовать его в своем public github репозитории.  Пайплайн должен содержать:
Steps:
- Скачивает любой публичный demo-nodejs проект с Github
- Производит его сборку и проверку(если тесты присутствуют)
- Разворачивает его в любом AWS аккаунте (для проверки будет использоваться новый AWS аккаунт) на существующем или новосозданном EC2 инстансе или в ECS
- Отправляет пост-билд результат на почту
### **Notes:**
В пайплайне можно использовать bash скрипты, докер, переменные окружения,  aws cli, etc. Пайплай должен запускаться на новосозданном Jenkins (можно использовать любые Jenkins plugins, но их список добавьте в readme Вашего репозитория
### **Manual:**
Создаем pipeline, указываем ссылку на гит, аккаунт с паролем и файл Jenkins.
![Advanced_Project_Options](https://github.com/resident33/Jenkins-Dev-pro/blob/master/src/Advanced_Project_Options.jpg)

Далее запускаем Build. Так как pipeline использует параметры первый запуск пройдет со статусом Fail. Все норм так задуманно ;)
![Build_Fail](https://github.com/resident33/Jenkins-Dev-pro/blob/master/src/Build_Fail.jpg)

При втором запуске появиться пункт Build with Parameters.


![Build_with_Parameters](https://github.com/resident33/Jenkins-Dev-pro/blob/master/src/Build_with_Parameters.jpg)

Вводим параметры:
DNS имя или Ip сервера где будем собирать и разворачивать апи.

Имя пользователя у которого есть доступ по ssh на сервер.

И ключ для подключения к серверу. (Скопировать и вставить внутрянку)

Запускаем Build
![Build_with_Parameters2](https://github.com/resident33/Jenkins-Dev-pro/blob/master/src/Build_with_Parameters2.jpg)

Как видим все прошло хорошо.
![Build_Success](https://github.com/resident33/Jenkins-Dev-pro/blob/master/src/Build_Success.jpg)
