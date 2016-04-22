# ssh-private-key-buildpack

A Heroku buildpack for setting the ssh private key as part of the application build. It's meant to be used as part of a setup [using multiple buildpacks](https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app), so other buildpacks can authenticate with hosts using ssh keys, for instance to install dependencies from private git repositories.

# Example usage

Add the buildpack to your Heroku app. In the example below the `ssh-private-key-buildpack` runs before the `heroku/go` buildpack.

```
heroku buildpacks:set --index 1 https://github.com/debitoor/ssh-private-key-buildpack.git
heroku buildpacks:add heroku/go
```

Set the private key environment variable `SSH_KEY` of your Heroku app (note that the key needs to be base64 encoded).

```
heroku config:set SSH_KEY=$(cat path/to/your/keys/id_rsa | base64)
```

By default the buildback adds Github to the `known_hosts`. However you can configure your app to add custom hosts, too. All that's needed is the set `SSH_HOSTS` for you app to a comma-separated list of hosts, e.g. ``

```
heroku config:set SSH_HOSTS="git@github.com,example.com"
```
