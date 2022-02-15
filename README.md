# Dockerizing Commands

- [PHP](php)
  - [Available Versions](#available-versions)
  - [Setting alias](#setting-alias)
    - [Without SSH](#without-ssh)

## About

The idea of this project is dockerizing the language commands, to be
not more necessary had installed the languages on the machine 
to run simple commands

## PHP

### Available versions:

- **7.3** - **omarkdev/cli-php:7.3**
- **8.1** - **omarkdev/cli-php:8.1**

All versions include composer command.

### Setting alias

You can set up the alias:

```bash
alias php="docker run --rm --tty -it \
    -u $(id -u):$(id -g) \
    -v $(pwd):/app \
    -v $HOME/.ssh:/home/sammy/.ssh \
    -w /app \
    omarkdev/cli-php:8.1 \
    php"

alias composer="docker run --rm --tty -it \
    -u $(id -u):$(id -g) \
    -v $(pwd):/app \
    -v $HOME/.ssh:/home/sammy/.ssh \
    -w /app \
    omarkdev/cli-php:8.1 \
    composer"
```

These alias are the most basic, including: non-root user and 
copy ssh keys to inside the container. It's important to see the alias 
will sync the volume to folder where the command as ran, so it's basically 
to you run commands to specific projects, but feel free to change.

The basic command include a copy of ssh to inside the container to 
allow installing private repositories.

#### Without SSH

You can set up the alias without ssh copy too:

```bash
alias php="docker run --rm --tty -it \
    -u $(id -u):$(id -g) \
    -v $(pwd):/app \
    -w /app \
    omarkdev/cli-php:8.1 \
    php"

alias composer="docker run --rm --tty -it \
    -u $(id -u):$(id -g) \
    -v $(pwd):/app \
    -w /app \
    omarkdev/cli-php:8.1 \
    composer"
```
