# Texto Explicativo

### O que cada Dockerfile faz

###### *products/Dockerfile*

- **FROM node:18-alpine**: Usa uma imagem do Node.js.
- **WORKDIR /app**: Define o diretório de trabalho.
- **COPY index.js .**: Copia o arquivo do app para o container.
- **RUN npm init -y**: Inicia um projeto Node.js.
- **RUN npm install express**: Instala o Express.
- **EXPOSE 3001**: Expõe a porta 3001.
- **CMD ["node", "index.js"]**: Comando para iniciar o app.
´´

###### *orders/Dockerfile* 
´´
- **FROM python:3.11-alpine**: Usa uma imagem do Python.
- **WORKDIR /app**: Define o diretório de trabalho.
- **COPY app.py .**: Copia o código do app. 
- **RUN pip install**: Instala dependências Python.
- **EXPOSE 3002**: Expõe a porta 3002.
- **CMD ["python", "app.py"]**: Comando para iniciar o app.
´´

###### *payments/Dockerfile* 

- **FROM php:8.1-cli**: Usa uma imagem do PHP.
- **WORKDIR /app**: Define o diretório de trabalho. 
- **COPY index.php .**: Copia o código do app.
- **EXPOSE 3003**: Expõe a porta 3003.
- **CMD ["php", "-S", "0.0.0.0:3003"]**: Inicia o servidor embutido do PHP.
´´

#### O que cada elemento do docker-compose.yml faz

**services**: Define os serviços que serão criados
´´
**products**: Serviço do app de produtos
´´
**build**: Usa o dockerfile da pasta products
´´
**ports**: Mapeia a porta 3001 do container para a máquina
´´
**networks**: Conecta a rede app-network
´´
**orders**: Serviço do app de pedidos
´´
**build**: Usa o dockerfile da pasta orders
´´
**ports**: Mapeia a porta 3002
´´
**depends_on**: Só inicia depois de products, db e redis
´´
**environment**: Variáveis de ambiente para conexão com MySQL e Redis
´´
**networks**: Conecta a rede app-network
´´
**payments**: Serviço do app de pagamentos
´´
**build**: Usa o Dockerfile da pasta payments
´´
**ports**: Mapeia a porta 3003
´´
**depends_on**: Só inicia depois de orders
´´
**networks**: Conecta a rede app-network
´´
**db**: Serviço do banco de dados MySQL
´´
**image**: Usa a imagem oficial do MySQL
´´
**environment**: Define senha e banco
´´
**ports**: Mapeia a porta 3307 da máquina para 3306 do container
´´
**volumes**: Persiste dados em db-data
´´
**networks**: Conecta a rede app-network
´´
**redis**: Serviço do Redis
´´
**image**: Usa a imagem oficial do Redis
´´
**ports**: Mapeia a porta 6379
´´
**networks**: Conecta a rede app-network
´´
**volumes**: Define volumes persistentes
´´
**networks**: Define a rede app-network para comunicação entre os serviços
