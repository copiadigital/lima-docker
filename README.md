# Supported tags and respective `Dockerfile` links

-	[`7.0-apache`, (*php/7.0/apache/Dockerfile*)](https://github.com/CopiaDigital/lima-docker/blob/master/php/7.0/apache/Dockerfile)
-	[`5.6-apache`, (*php/5.6/apache/Dockerfile*)](https://github.com/CopiaDigital/lima-docker/blob/master/php/5.6/apache/Dockerfile)


# What is Lima?

Lima is a PHP CMS written and used by [Copia Digital](http://www.copiadigital.co.uk)

# How to use this image.

## With Command Line

For Lima projects run through the command line interface (CLI), you can do the following.

### Create a `Dockerfile` in your Lima project

```dockerfile
FROM copia/lima:5.6-apache
COPY . /usr/src/lima
```

Then, run the commands to build and run the Docker image:

```console
$ docker build -t my-lima-app .
$ docker run -it --name my-running-app my-lima-app
```

### Making changes (in development)

To use your native IDE, and see the changes instantly on the docker version, mount your Lima directory as a volume on run. From the root project folder, you would run:

$ docker run -it --name my-running-app -v "$PWD":/usr/src/lima copia/lima:5.6-apache

### Run a single PHP script

For many tasks, like updating packages or running phing, it is easier to use the image. In such cases, you can run a command by using the Docker image directly:

```console
$ docker run -it --rm --name my-running-script -v "$PWD":/usr/src/lima copia/lima:5.6-apache composer install
```

## With Docker Compose

Take a look at our sample docker-compose.yml files for each version, for getting an instance of Lima set up with MYSQL too.