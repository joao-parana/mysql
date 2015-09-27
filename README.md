# mysql

> Imagem Docker para MySQL 5.6.26 rodando no Debian Jessie (version 8)

Usado no curso [http://joao-parana.com.br/blog/curso-docker/](http://joao-parana.com.br/blog/curso-docker/) criado para a Escola Linux.


Veja no Diagrama abaixo o contêiner e seu nome, os arquivos de inicialização durante o start e a porta do MySQL

![https://raw.githubusercontent.com/joao-parana/mysql/master/docs/jessie-mysql.png](https://raw.githubusercontent.com/joao-parana/mysql/master/docs/jessie-mysql.png)


Criando a imagem

    docker build -t HUB-USER-NAME/mysql  .

Substitua o token `HUB-USER-NAME` pelo seu login em [http://hub.docker.com](http://hub.docker.com)


Usaremos aqui o nome `mysql_db` para o Contêiner.
Caso exista algum conteiner com o mesmo nome rodando, 
podemos pará-lo assim:

    docker stop mysql_db

> Pode demorar alguns segundos para parar e isto é normal.

Em seguida podemos removê-lo

    docker rm mysql_db

Podemos Executar o Contêiner como Daemon assim:

    docker run -d --name mysql_db -p 9306:3306 HUB-USER-NAME/mysql

Observe o mapeamento da porta 3306 do MySQL dentro do contêiner 
para uso externo em 9306. O valor 9306 pode ser alterado a seu critério.

Verificando o Log

    docker logs mysql_db

Após executar o sistema por um tempo, podemos parar o contêiner 
novamente para manutenção

    docker stop mysql_db

e depois iniciá-lo novamente e observar o log

    docker start mysql_db && sleep 5 && docker logs mysql_db

Observe que **o LOG é acumulativo** e que agora não é executado o 
processo de Inicialização do Database, criação de usuários no MySQL, 
criação do nosso database, etc. 

Você poderá ver o conteúdo do diretório /tmp executando o comando abaixo:

    docker exec mysql_db ls -lat /tmp

Se você estiver usando o MAC OSX com Boot2Docker 
poderá executar o comando abaixo para abrir uma sessão como 
root no MySQL:

    mysql -h `boot2docker ip` -u root -p -P 9306

A senha está Hard-coded no arquivo run.sh
apenas por motivos didáticos. Veja a variável `MYSQL_ROOT_PASSWORD`


Mais detalhes sobre Docker no meu Blog: [http://joao-parana.com.br/blog/](http://joao-parana.com.br/blog/)
