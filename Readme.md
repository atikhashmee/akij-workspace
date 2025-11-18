copy these files where your projects resides

for example
  if your projects are in
   development
      -build/
      -amadeus/
      -zenith/

now based on your preference

### development

`cp docker-compose-development.yml compose.yml`

### production

`cp docker-compose-production.yml compose.yml`

then run

```
127.0.0.1        akijair.test
127.0.0.1        core-app.akijair.test
127.0.0.1        b2c-web.akijair.test
127.0.0.1        zenith.akijair.test
127.0.0.1        amadeus.akijair.test
127.0.0.1        payment.akijair.test
127.0.0.1        core-api.akijair.test
127.0.0.1        supplierhub.akijair.test

```

-- update this to your hosts file,
normally in linux/mac osx hosts file resides in /etc/hosts

for windows its under system32 directory

once you are done with above all these,
make sure you update all of your .env files.
just keep the note that for production build it will be
/build directory where the .env will be read.
if development every projects .env will be considerate

```
 docker compose up --build

```

now you can use these projects
