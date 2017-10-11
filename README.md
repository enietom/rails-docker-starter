# rails-docker-starter
Starter setup to create a Rails project using docker

## Credits
Most of this setup was taken from the [Docker Compose Documentation](https://docs.docker.com/compose/rails/).

## How to use this
* The first thing to do is clone this project.
* Then copy the files: `docker-compose.yml`, `Dockerfile`, `Gemfile` and `Gemfile.lock` to another
folder. Put the name of your app as the name of the folder.
* Using your terminal (or Docker Terminal if you are in Windows) navigate to the new folder and
generate the Rails skeleton app:

   `docker-compose run web rails new . --force --database=postgresql`
* Then build the image

   `docker-compose build`
* Now we have to update Rails so it points to out docker postgres image. Replace the contents
of `config/database.yml` with:

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
  database: <NAME-OF-YOUR-APP>_development

test:
  <<: *default
  database: <NAME-OF-YOUR-APP>_test
```
   Where `<NAME-OF-YOUR-APP>` is the name you used in the second step.
* Finally, boot the app with:

   `docker-compose up`

   And go to http://localhost:3000 to find Rails' Welcome Page (if you are using Docker Machine
   you'll need to go to `http://<IP-OF-YOUR-DOCKER-MACHINE>:3000`)
