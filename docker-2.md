# Практическая работа по теме Практическое применение Docker #  
## Задача 0 ##  
Создал ВМ Ubuntu 20  
![docker compose не установлен](docker-2-1.jpg)  
Установил свежий docker-compose  
![Установлен docker compose](docker-2-2.jpg)  
## Задача 1  ##  
### Создал fork репозитория  ###  
https://github.com/uxtuahgp/shvirtd-example-python/tree/main  
### Скопировал и дополнил Dockerfile.python ###  
https://github.com/uxtuahgp/shvirtd-example-python/blob/main/Dockerfile.python  
### Создал файл .dockerignore ###   
https://github.com/uxtuahgp/shvirtd-example-python/blob/main/.dockerignore  
### Склонировал репозиторий на ВМ ###   
git clone https://github.com/uxtuahgp/shvirtd-example-python/tree/main  
Далее при изменениях 
docker compose down -d; sudo rm -rf ./data  
git pull  
### Сборка проекта ###
docker build --tag docker-2:latest -f Dockerfile.python .
![Сборка Docker образа](docker-2-3.jpg)
### Запуск docker compose 
При попытке запуска приложение python падало, как в результате я понял, из-за того, что на момент его запуска БД еще не была готова.  
depends_on не помогало. Вероятно надо было покрутить хелсчек, но я решил просто поставить задержку 30 секунд в wait.sh с последующим запуском uvicorn main:app...  
wait.sh установил в качестве entrypoint в compose.yaml  
Для соединения с сервисами прокси использовал include  
![Запусл docker compose](docker-2-4.jpg)  
![Результат docker compose](docker-2-5.jpg)  
## Задача 1.3 * ##
Для запуска приложения на ВМ  
### Установил python3.8-venv ###  
sudo apt install python3.8-venv  
### Создал виртуальное окружение  ###  
python3 -m venv venv  
source venv/bin/activate  
### Установил зависимости ###  
pip install -r requirements.txt  
### Установил переменные окружения для запуска приложения ###  
export DB_HOST='127.0.0.1'    
export DB_USER='app'  
export DB_PASSWORD='very_strong'  
export DB_NAME='example' 
export DB_TABLE='reqs'
### Запустил сервер MySQL в контейнере ###  
Для venv писался отдельный compose с единственным сервисом mysql
### Запустил uvicorn ###
uvicorn main:app --host 0.0.0.0 --port 5000 --reload
![Запуск uvicorn локально в venv](docker-2-6.jpg)  
## Задача 3.2 * ##  
Добавил в compose.yaml переменную DB_TABLE  
В коде main.py добавил извлечение в переменную из переменной среды  
db_table = os.environ.get('DB_TABLE', 'requests')  
В трех запросах вместо статического текст добавил заначения из контстанты.  
db_table = os.environ.get('DB_TABLE', 'requests')  

query = "INSERT INTO "+db_table+" (request_date, request_ip) VALUES (%s, %s)"  

query = "SELECT id, request_date, request_ip FROM "+db_table+" ORDER BY id DESC LIMIT 50"  
# Задача 2 #
![Работа с Yandex registry](docker-2-7.jpg)  

# Задача 3 #  
![Работа с Yandex registry](docker-2-7.jpg)  
