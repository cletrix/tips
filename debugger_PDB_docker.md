#Executando o módulo debugger PDB do Python com o docker.
- **2017 11 30** 
- **Cleyton Pedroza**


### Prepare
Para resolvermos esse problema devemos adicionar o suporte a interação do usuário no containner que queremos interagir. PAra isso devemos mudar o arquivo docker-compose.yml para dar suporte a interação com o usuário, adicionando:

	stdin_open: true 
	tty: true

exemplo de um docker-compose:

	version: '3'		
	services:
	    demo_web:
	        build:
	            context: .
	            dockerfile: demo_web/Dockerfile
	        ports:
	            - "80:8000"
	        command: /usr/local/bin/gunicorn -w 2 -t 3600 -b :8000 app:app --reload
	        volumes:
	            - ./demo_web:/usr/src/app
	        stdin_open: true
	        tty: true
### PDB
Devemos colocar o nosso break-point de forma padrão no código. 
	
	import pdb;pdb.set_trace()

Podemos ter algo como :

	from flask import Flask
	app = Flask(__name__)
	
	@app.route('/')
	def hello_pdb():
	    message = 'Hello Docker'
	    import pdb; pdb.set_trace()
	    return message
	    
### Debugging

Agora podemos usar : 

	docker-compose up -d --build 

Para reinicializar o docker, lembrando que ao usarmos o -d estaremos em **detached mode**. Ou seja estaremos rodando em background.



### Monitor
Com o docker-compose em funcionamento, devemos descobrir o numero do CONTAINER ID ou o nome em NAMES, com o comando:
	
	docker ps
	
Devemos conectar ao processo:

	docker attach CONTAINER_ID
	
ou 

	docker attach NAMES


__Referencia para este documento :__ [blog.lucasferreira.org] (https://blog.lucasferreira.org/howto/2017/06/03/running-pdb-with-docker-and-gunicorn.html)