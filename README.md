# Após "buildar" o projeto e localizar o dist:
## Crie um diretornio nginx e nele crie o arquivo nginx.conf
### Adicione o conteudo

<a href="./nginx.conf"><code>nginx.conf</code></a>

# Crie uma rede local para os containers

`docker network create minha-rede`

# Após isso crie o container loadbalancer

`docker run -d --name loadbalancer --network minha-rede -p 8080:80 -v /caminho/para/nginx/nginx.conf:/etc/nginx/nginx.conf:ro nginx:alpine`

# Crie os nós que precisar
## Lembre-se: 
* Apontar para o local do arquivo com o build do sistema que vai usado
* Mudar o nome do container que será nó

`docker run -d --name node1 --network minha-rede -v /caminho/para/dist:/usr/share/nginx/html:ro nginx:alpine`

# Após criar os nós
* Altere os default.conf de cada nó
* Mudando para: 

<a href="./default.conf"><code>default.conf</code></a>

### Utilitario
* Se a imagem for baseada em Alpine Linux:

`apk update && apk add nano (vim ou vi)`

* Ver logs em tempo real

`docker logs-f loadbalancer`
