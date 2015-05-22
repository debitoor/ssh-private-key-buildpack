# ssh-private-key-buildpack

A heroku buildpack for setting the ssh private key as part of the application build. It's meant to be used with [heroku-buildpack-multi](https://github.com/heroku/heroku-buildpack-multi), before other buildpacks which require the key to be present, like installing private `npm` modules from `github`.

# Example usage

Upload the private key to heroku (note that the key needs to be base64 encoded).

```
heroku config:set SSH_KEY=$(cat ~/.ssh/id_rsa | base64)
```

Add a `.buildpacks` file (used by `heroku-buildpack-multi`) which contains this and the default node.js buildpack.

```
https://github.com/debitoor/ssh-private-key-buildpack.git#v1.0.0
https://github.com/heroku/heroku-buildpack-nodejs.git#v75
```

Now as long as the public key is present on github and the user has the correct permissions, it's possible to install `npm` modules from private `githup` repositories.
