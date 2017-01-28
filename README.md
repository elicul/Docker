## Docker instalacija

Upute za instalaciju Dockera na Ubuntu 26.04.

Ažuriranje databaze instalacijskih paketa

```bash
	sudo apt-get update
``` 

Dodavanje GPG ključa za dodavanje DOcker repozitorija

```bash
	sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
``` 

Dodavanje repozitorija unutar APT

```bash
	sudo apt-add-repository 'deb https://apt.dockerproject.org/repo ubuntu-xenial main'
``` 

Ažuriranje databaze instalacijskih paketa

```bash
	sudo apt-get update
``` 

Dodavanje police Docker repozitorija

```bash
	apt-cache policy docker-engine
``` 

Nakon navedene komande potrebno je dobiti sljedeći output

```bash
	docker-engine:
	  Installed: (none)
	  Candidate: 1.11.1-0~xenial
	  Version table:
	     1.11.1-0~xenial 500
	        500 https://apt.dockerproject.org/repo ubuntu-xenial/main amd64 Packages
	     1.11.0-0~xenial 500
	        500 https://apt.dockerproject.org/repo ubuntu-xenial/main amd64 Packages
```

Instalacija Dockera
```bash
	sudo apt-get install -y docker-engine
```

Povjera da je Docker uspješno instaliran i pokrenut

```bash
	sudo systemctl status docker
```

Potrebno je dobiti sljedeći output

```bash
	docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: active (running) since Sun 2016-05-01 06:53:52 CDT; 1 weeks 3 days ago
     Docs: https://docs.docker.com
 Main PID: 749 (docker)
```

Dodjela usera unutar Docker grupe

```bash
	sudo usermod -aG docker $(whoami)
```

## Docker Compose instalacija

Kako bi mogli instalirati Docker Compose prije moramo imati instaliran **python-pip**

```bash
	sudo apt-get -y install python-pip
```

Instalacija **docker-compose** paketa

```bash
	sudo pip install docker-compose
```

## Kreacija direktorija s Docker Compose **.yaml** datotekom

Kreiramo direktorij a zatim izrađujemo **docker-compose.yml**

```bash
	mkdir wordpress
	cd wordpress
	nano docker-compose.yml
```

Unutar **docker-compose.yml** zalijepimo sljedeći kod 

```yaml
	version: '2'
	services:
	  wordpress:
	    image: wordpress:latest
	    networks:
	      - front
	      - back
	    ports:
	      - 8080:80
	    environment:
	      WORDPRESS_DB_PASSWORD: examplepass
	      WORDPRESS_DB_NAME: wpdb
	      WORDPRESS_TABLE_PREFIX: wp_
	      WORDPRESS_DB_HOST: wordpress_db
	    volumes:
	      - ./wordpress-data:/var/www/html
	      - ./php/uploads.ini:/usr/local/etc/php/conf.d/uploads.ini
	  wordpress_db:
	    image: mariadb:latest
	    environment:
	      MYSQL_ROOT_PASSWORD: examplepass
	    volumes:
	      - wordpress-db-data:/var/lib/mysql
	    networks:
	      - back
	  phpmyadmin:
	    image: phpmyadmin/phpmyadmin:latest
	    networks:
	      - back
	    ports:
	      - 8181:80
	    environment:
	      MYSQL_USERNAME: root
	      MYSQL_ROOT_PASSWORD: examplepass
	      PMA_HOST: wordpress_db
	volumes:
	    wordpress-db-data:
	      driver: local
	networks:
	  front:
	  back:
```

U istom direktoriju sada pokrenemo sljedeću naredbu kako bi pokrenuli naš Wordpress s PhpMyAdminom i MariaDB databazom

```bash
	docker-compose up
```

Navedene Docker kontejnere zaustavljamo s naredbom 

```bash
	docker-compose stop
```