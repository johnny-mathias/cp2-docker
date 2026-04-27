# HOW TO - DOCKER 


### No CMD, dentro de /movies: 
scp target/movies-0.0.1-SNAPSHOT.jar admLnx@SEUIPDAVM:/home/admLnx

// ip do meu grupo: 20.220.222.177
// usamos o mesmo usuário e senha do professor nas aulas

---

## Agora no Alma Linux:


### Criar rede

sudo docker network create rede-rm563409

### Criar volume nomeado

sudo docker volume create mysql-data-rm563409

### Subir Container do MySQL 

sudo docker run -d \
--name mysql-rm563409 \
--network rede-rm563409 \
-p 3306:3306 \
-e MYSQL_ROOT_PASSWORD=root123 \
-e MYSQL_DATABASE=moviesdb \
-e MYSQL_USER=user \
-e MYSQL_PASSWORD=user123 \
-v mysql-data-rm563409:/var/lib/mysql \
mysql:8.0

### Subir Container da Aplicação 

sudo docker run -d \
--name app-rm563409 \
--network rede-rm563409 \
-p 8080:8080 \
-e SPRING_DATASOURCE_URL=jdbc:mysql://mysql-rm563409:3306/moviesdb \
-e SPRING_DATASOURCE_USERNAME=user \
-e SPRING_DATASOURCE_PASSWORD=user123 \
-v /home/admLnx/movies-0.0.1-SNAPSHOT.jar:/app/app.jar \
eclipse-temurin:17-jdk \
java -jar /app/app.jar

### Entrar no container do MySQL 

sudo docker exec -it mysql-rm563409 mysql -u root -p

### Ele vai pedir a senha:

root123 

### Selecionar o banco

USE moviesdb;

### Criar uma tabela manualmente 

CREATE TABLE movie (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255),
    synopsis VARCHAR(255),
    rating INT,
    release_date DATE
);

### Verificar 
SHOW TABLES;

---

## CRUD

### Crud - Create (POST) 

INSERT INTO movie (title, synopsis, rating, release_date)
VALUES (
    'Interestelar',
    'Viagem espacial em busca de um novo lar para a humanidade',
    10,
    '2014-11-06'
);


### cRud - READ (GET)

SELECT * FROM movie;

#### crUd - UPDATE (PUT)

UPDATE 
UPDATE movie
SET rating = 9
WHERE id = 3;

### Confirmar alteração 

SELECT * FROM movie;

### cruD - Delete (DEL)

DELETE 
DELETE FROM movie
WHERE id = 3;

### Confirmar exclusão

SELECT * FROM movie;

---

## 📼 Link do Vídeo no Youtube:

https://www.youtube.com/watch?v=6cu1bAZPPwQ
