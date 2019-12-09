Задание:
Подготовить Jenkinsfile и опубликовать его в своем public github репозитории.  Пайплайн должен содержать:
   Steps: 
- Скачивает любой публичный demo-nodejs проект с Github
- Производит его сборку и проверку(если тесты присутствуют)
- Разворачивает его в любом AWS аккаунте (для проверки будет использоваться новый AWS аккаунт) на существующем или новосозданном EC2 инстансе или в ECS
- Отправляет пост-билд результат на почту

В пайплайне можно использовать bash скрипты, докер, переменные окружения,  aws cli, etc. Пайплай должен запускаться на новосозданном Jenkins (можно использовать любые Jenkins plugins, но их список добавьте в readme Вашего репозитория