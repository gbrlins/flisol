# flisol
Hands on containers

Itinerários comandos apresentação docker:

Exemplo prático do NGINX. Ele é acessível pelo endereço público no EC2, ou de eth0 na VM:
*obs: a primeira porta é da máquina. Pode usar qualquer segundo IP, desde que ele esteja liberado*

docker run -d -p 80:80 nginx

Rodando o container do NGINX, é possível verificar algumas informações:
docker ps -a
docker rm <NAME>
docker rmi <IMG>
docker exec -ti amazing_williamson bash
	cat /etc/os-release
  
O mais legal é já subir um container com as informações alteradas
mkdir site-content
vim index.html

<!doctype html>
<html lang="pt">
<head>
  <meta charset="utf-8">
  <title>Bem-vindo ao Flisol</title>
</head>
<body>
  <h1>Olá, meus amigos!</h1>
        <h2>Esse é o meu primeiro container criado no evento Flisol.</h2>
        <img src="flisol.jpg" alt="Flisol">
</body>
</html>

wget http://www.gulag.org.mx/2021-03-19-invitacion_flisol/flisol-libre-software-logo.jpg 

docker run -ti -d -p 8080:80 --name meu-nginx -v ~/site-content/:/usr/share/nginx/html nginx

  
Só que, se eu deletar esse container... eu perdi todas as informações. Essa é a natureza efêmera do container. Criar um container do *nginx* seu pra não ter que ficar sempre fazendo esse procedimento.
  obs: Criar esse comando no mesmo diretório criado
  
docker rm -f $(docker ps -a -q)
vim Dockerfile

FROM nginx:latest
COPY ./index.html /usr/share/nginx/html/index.html
COPY ./flisol.jpg /usr/share/nginx/html/flisol.jpg

docker build -t webserver .
docker images
docker run -it -d -p 8080:80 --name meu-nginx webserver
  
Agora essa imagem está construída localmente e todas as dependências estão resolvidas e podem rodar em qualquer lugar.
  
  
