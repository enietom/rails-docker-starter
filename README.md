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

## Installing Javascript Libraries
The docker image you are creating should already have Yarn installed. For instance, if you would like to install JQuery, then you'd run (after running `docker-compose up`):

`docker-compose exec web yarn add jquery`

However, be aware that you still need to add these libraries in the `application.js` file.
## Further reading
Some sites that might be helpful once your Rails+Docker project is generated.
* [Rails Guides](http://guides.rubyonrails.org)
* [Bootstrap Ruby Gem](https://github.com/twbs/bootstrap-rubygem)
* [infinum.co - List of Commonly-used Gems](https://infinum.co/the-capsized-eight/a-gem-for-every-occasion-11-great-ruby-libraries-we-use-on-every-project)
* [Free Open Source Bootstrap Themes](https://startbootstrap.com/)
