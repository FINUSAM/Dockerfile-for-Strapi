# Setting up Strapi using Docker

### `Choose Dockerfile`

1. choose any of the 2 dockerfiles above based on your requirement. Development or Production.
2. copy the selected dockerfile
3. paste the copied file inside your strapi root directory
4. rename it to "Dockerfile"
5. build & run (individually or docker-compose) explained below

### `build & run manually`
build command:
```
docker build -t strapi-app .
```
mysql run command:
```
docker run -d --name strapi-db --network strapi-network -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=strapi -e MYSQL_USER=strapi -e MYSQL_PASSWORD=strapi -v strapi-db-data:/var/lib/mysql mysql:8.0 --default-authentication-plugin=mysql_native_password      
```
strapi run command (strapi requires 12 environment variables including mysql credentails to run):
```
docker run -d --name strapi-app --network strapi-network -p 1337:1337 -e DATABASE_CLIENT=mysql -e DATABASE_HOST=strapi-db -e DATABASE_PORT=3306 -e DATABASE_NAME=strapi -e DATABASE_USERNAME=strapi -e DATABASE_PASSWORD=strapi -e APP_KEYS="key1,key2,key3,key4" -e JWT_SECRET="superlongjwtsecret" -e ADMIN_JWT_SECRET="superlongadminjwtsecret" -e API_TOKEN_SALT="superlongapisalt" -e TRANSFER_TOKEN_SALT="superlongtransfersalt" -e ENCRYPTION_KEY="superlongencryptionkey" phazacrshareddev001.azurecr.io/strapi-app:dev
```

### `build & run using docker compose`
Move docker-compose.yml file to strapi root directory where Dockerfile is stored
```
docker-compose up
```
