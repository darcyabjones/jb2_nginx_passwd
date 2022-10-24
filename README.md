# JBrowse2 behind a login

This is a quick and dirty setup to put a website behind a password login.
It's developed to support sharing JBrowse2 servers with colleagues, where I don't want to necessarily share the data openly, but i'm also not really that bothered if someone determined cracks it.

## How to use.

1) Install the jbrowse2 CLI tools (https://jbrowse.org/jb2/docs/quickstart_cli/).
2) Setup a password file 
   ```
   sudo apt-get install apache2-utils
   touch ./htpasswd  # This just avoids having to use htpasswd -c the first time.
   # For each user run below
   htpasswd ./htpasswd USERNAME
   # The passwords are salted etc, but still, it's better to pretend to restrict it at least.
   chmod og-rwx ./htpasswd
   ```
   Try not to let this file get into version control.
3) Create the jbrowse project
   ```
   jbrowse create /home/user/jbrowse2
   ```
4) Add a bunch of stuff to your jbrowse project.
   Note that currently the data needs to be a subdirectory of the jbrowse project.
   It's possible to use a volume mount to get around this.


Next make sure that your `jbrowse2` and `htpasswd` files match what's in `docker-compose.yml`.
Then run.

```
docker-compose up
```

## Caveats

I originally thought this was going to be a lot harder than it was.
Mostly this just helps me remember how to do it.

There's a new version of docker compose that isn't installed by default on the servers i'm using.
This has a slightly different syntax and some new features.
It shouldn't be too hard to translate this to the new `docker compose` syntax.
