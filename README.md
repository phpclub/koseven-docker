# Koseven Docker Images
![License](https://img.shields.io/badge/license-BSD--3--Clause-green.svg)

This repository holds docker images which can be used for Koseven.

There will be 4 branches which all server a different purpose:

| Branch          | Purpose                                                                                 |
| --------------- | --------------------------------------------------------------------------------------- |
| master          | Image for a development/production environment.                                         |
| travis          | Image for Unit-Testing inside Travis CI (CAREFUL: Don't use on production servers.)     |
| devel           | Development Branch for `master`. Only latest `koseven:devel` version will be supproted. |
| travis-devel    | Development Branch for `travis`. Only latest `koseven:devel` version will be supproted. |

## Using the container images

Using one of the container is quite straight forward.
The docker repository for them is called `koseven/docker`.

By specifying the desired branch as docker-tag you can acquire the desired image.

_Note: for pulling the `master` branch use `latest` as tag name._

e.g. This will pull the master branch image:
`docker pull koseven/docker:latest`

e.g This will pull the travis branch image:
`docker pull koseven/docker:travis-devel`

After executing the `docker pull` command from above you're done setting up
your docker image, now you can go ahead and use it!

## Example for using `master` image

__Coming Soon. Stay tuned!__

## Example for using `travis-devel` image

For this particular Image you have multiple options. 

1. Some IDE's ([PHPStorm](https://blog.alejandrocelaya.com/2017/02/01/run-phpunit-tests-inside-docker-container-from-phpstorm/) for example) have full support for docker unittesting, you just need to configure it there and
   you are good to go!
   
2. Run the tests from the cli. Execute the following cli commands (from within your Koseven installation folder):
   Start container in background and mount installation folder:  

   ```shell
   docker run -dtP --name unittest -v $(pwd):/tmp/koseven/ koseven/docker:travis-devel
   ```

 3. Start services, install composer requirements and run PHPUnit  
   ```shell
   docker exec unittest /bin/sh -c "service redis-server start; cd /tmp/koseven; composer install; php vendor/bin/phpunit --globals-backup"
   ```
   
_(Hint) You can execute a `/bin/bash` shell inside the container and modify it before Unit-Testing  
```shell
docker exec -it unittest /bin/bash
```
_(Hint) You can execute a single test
```shell
docker exec -it unittest /bin/bash
service redis-server start; cd /tmp/koseven; composer install;
php vendor/bin/phpunit   --filter HTMLTest
php vendor/bin/phpunit   --filter HTMLTest --debug 
```
_

For more examples / tutorials how to create and interact with container visit the official [Docker Help](https://docs.docker.com/get-started/)

## Roadmap

| Target                 | Release date |
| ---------------------- |--------------|
| Initial `master` image | 2024.07.?? |
| Initial `travis` image | 2024.06.01   |
| Initial `travis-devel` | 2024.05.23   |

## Contributing

As usual, [fork and send pull requests](https://help.github.com/articles/fork-a-repo)

## Getting Help

* Open issues in this project.