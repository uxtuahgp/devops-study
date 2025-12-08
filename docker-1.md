# Практическая работа по теме "Оркестрация группой Docker контейнеров на примере Docker Compose." #
## Задача 1 ##
https://hub.docker.com/repository/docker/uxtuahgp/custom-nginx/general
## Задача 2 ##
\# date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html  

08-12-2025 20:59:50.210979632 MSK  
CONTAINER ID   IMAGE                         COMMAND                  CREATED         STATUS         PORTS                                     NAMES  
4b9c604efcaa   uxtuahgp/custom-nginx:1.0.0   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   custom-nginx-t2  
172.17.0.1 - - [08/Dec/2025:17:57:32 +0000] "GET / HTTP/1.1" 200 95 "-" "curl/7.81.0" "-"  
PGh0bWw+CjxoZWFkPgpIZXksIE5ldG9sb2d5CjwvaGVhZD4KPGJvZHk+CjxoMT5JIHdpbGwgYmUg  
RGV2T3BzIEVuZ2luZWVyITwvaDE+CjwvYm9keT4KPC9odG1sPgo=  
### Проверка ###
\# date +"%d-%m-%Y %T.%N %Z" ;curl http://uxtu-note:8080  
08-12-2025 21:04:42.702055776 MSK  
<html>  
<head>  
Hey, Netology  
</head>  
<body>  
<h1>I will be DevOps Engineer!</h1>  
</body>  
</html>  
<img src=https://github.com/uxtuahgp/devops-study/blob/main/docker-1-1.jpg> Snap 1 </img>  

## Задача 3 ##   
<img src=>https://github.com/uxtuahgp/devops-study/blob/main/docker-1-3-1.jpg</img>  
Контейнер остановился так как мы в стандартный поток ввода подали сигнал прерывания процесса.  
<img src=>https://github.com/uxtuahgp/devops-study/blob/main/docker-1-3-2.jpg</img>  
Мы на работающем контейнере изменили прослушиваемый NGINX порт на 81, но мэпинг портов не поменяли. 
Переадресация осталась 8080 -> 80, но внутри контейнера 80 порт никто уже не слушал. 

