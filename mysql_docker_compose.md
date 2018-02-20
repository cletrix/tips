## Docker-compose para o MySQL com volume compartilhado
- **2018 02 01** 
- **Cleyton Pedroza**

exemplo do docker-compose:

	version: '3.1'
		services:
		  db:
		    image: mysql
		    restart: always
		    environment:
		      MYSQL_ROOT_PASSWORD: python
		    ports:
		      - 3306:3306  
		    volumes:
		      - /opt/docker/mysql:/var/lib/mysql

		  adminer:
		    image: adminer
		    restart: always
		    ports:
		      - 9080:8080
