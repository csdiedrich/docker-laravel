# docker-compose-laravel
Pojeto simplificado de uso do docker para criar um stack laravel local totalmente funcional, obrigado @aschmelyun pelo conteúdo.

## Uso

Depois de clonado o projeto, acesse a pasta do projeto e execute no terminal:

`docker-compose build`

`docker-compose up -d`

O docker-compose subirá os seguintes serviços e portas em seu computador:

- **nginx** - `:8080`
- **mysql** - `:3306`
- **php** - `:9000`

# Criando uma app

Primeiramente remova todos os arquivos da pasta src/ e define o seguinte usuário como dono da mesma:

`chown 1000 src -Rf`

Em seguinte crie seu projeto com o comando:

`docker-compose run --rm composer create-project laravel/laravel .`

Neste projeto temos ainda mais três containers com ferramentas que você não precisará ter instalado em sua máquina, são elas: Composer, NPM, e Artisan. Utilize os seguintes comandos para utilizá-las:

- `docker-compose run --rm composer update`
- `docker-compose run --rm npm run dev`
- `docker-compose run --rm artisan migrate` 

## Persistindo MySQL

Por padrão, sempre qe você parar essa stack os dandos armazenados no banco de dados MySQL serão perdidos, pois os mesmos estão dentro do container que será removido. Caso você tenha necessidade de persistir essas informações, siga os passos:

1. Crie uma pasta chamado `mysql` na raiz do projeto, assim como tem a `nginx` e `src`.
2. Modifique o serviço `mysql` dentro do `docker-compose.yml` adicionando ao final da parte de network as seguintes lindas:

```
volumes:
  - ./mysql:/var/lib/mysql
```