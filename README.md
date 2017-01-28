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