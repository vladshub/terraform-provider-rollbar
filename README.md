Terraform Provider
==================

- Website: https://www.terraform.io
- [![Gitter chat](https://badges.gitter.im/hashicorp-terraform/Lobby.png)](https://gitter.im/hashicorp-terraform/Lobby)
- [![Build Status](https://travis-ci.org/babbel/terraform-provider-rollbar.svg?branch=master)](https://travis-ci.org/babbel/terraform-provider-rollbar)
- Mailing list: [Google Groups](http://groups.google.com/group/terraform-tool)

<img src="https://cdn.rawgit.com/hashicorp/terraform-website/master/content/source/assets/images/logo-hashicorp.svg" width="600px">

Requirements
------------

- [Terraform](https://www.terraform.io/downloads.html) 0.10.x
- [Go](https://golang.org/doc/install) 1.10.x+ (to build the provider plugin)

Building The Provider
---------------------
Clone repository to: `$GOPATH/src/github.com/babbel/terraform-provider-rollbar`

```sh
$ mkdir -p $GOPATH/src/github.com/babbel; cd $GOPATH/src/github.com/babbel
$ git clone git@github.com:babbel/terraform-provider-rollbar
```

Enter the provider directory and build the provider

```sh
$ cd $GOPATH/src/github.com/babbel/terraform-provider-rollbar
$ make build
```

Using the provider
----------------------

```hcl
provider "rollbar" {
  api_key = "${var.api_key}"
}

resource "rollbar_user" "test" {
  team_id = 333290
  email   = "test@somewhere.com"
}
```

Developing the Provider
---------------------------

If you wish to work on the provider, you'll first need [Go](http://www.golang.org) installed on your machine (version 1.10.x+ is *required*). You'll also need to correctly setup a [GOPATH](http://golang.org/doc/code.html#GOPATH), as well as adding `$GOPATH/bin` to your `$PATH`.

To compile the provider, run `make build`. This will build the provider and put the provider binary in the `$GOPATH/bin` directory.

```sh
$ make bin
...
$ $GOPATH/bin/terraform-provider-rollbar
...
```

In order to test the provider, you can simply run `make test`.

```sh
$ make test
```
We cannot have the acceptance tests until rollbar changes/improves their api.
The reason is because creating an invitation doesn't yield an userid.
A user id is created when a user accepts their invitation.

Github Releases
---------------------------
In order to push a release to Github the feature branch has to merged into master and then a tag needs to be created with the version name of the provider e.g. **v0.0.1** and pushed.

```sh
git checkout master
git pull origin master
git tag v<semver> -m "release comment"
git push origin master --tags
```
