# dockerails

A barebones Rails 5 app running in a Docker container.

## Getting up and running

### Build

Build the container while in the root directory of this project

```sh
$ docker build -t dockerails .
```

### Run

Run the rails server on the container and point port 3000 in the container to the local port 3000.

```sh
$ docker run -it --rm -p 3000:3000 dockerails rails s
```

You should now be able to see the rails welcome page when visiting http://localhost:3000

## Recreating this app

### Summary

1. Create a new rails app
2. Create a `Dockerfile`

## Requirements

1. Ruby installed - version 2.3.3 was used here installed via RVM - `rvm install 2.3.3`
2. Rails gem insatlled - version 5.0.1 was used here - `gem install rails`
3. Docker installed - version 1.13.1 was used here

### Commands

Create a new rails app and a Dockerfile

```sh
$ rails new dockerails .
      create
      create  README.md
      create  Rakefile
      create  config.ru
      create  .gitignore
..
$ cd dockerails
$ touch Dockerfile
```

Add the following to the Dockerfile. The first run command uses the apt-get package manager to install packages required for building some gems. The second run command installs the gems specified in the Gemfile that was created by rails.

```dockerfile
# Dockerfile
FROM ruby:2.3.3-onbuild

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

RUN bundle install
```

## Resources

- [Docker Hub Ruby Page](https://hub.docker.com/_/ruby)
- [RVM](https://rvm.io)
