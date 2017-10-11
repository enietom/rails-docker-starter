# rails-docker-starter
Starter setup to create a Rails project using docker

## Credits
Most of this setup was taken from the [Docker Compose Documentation](https://docs.docker.com/compose/rails/).

## Commands
* First generate the Rails skeleton app:

   `docker-compose run web rails new . --force --database=postgresql`
* Then build the image

   `docker-compose build`
* Now we have to update Rails so it points to out docker postgres image. Replace the contents of `config/database.yml` with:

```yml
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password:
  pool: 5

development:
  <<: *default
  database: myapp_development

test:
  <<: *default
  database: myapp_test
```

* Finally, boot the app with:

   `docker-compose up`
