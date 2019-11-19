# helm quay plugin

## Install the helm quay Plugin

First, Install the latest [Helm release](https://github.com/kubernetes/helm#install).

If you are an OSX user, quickstart with brew: `brew install kubernetes-helm`

Next download and install the registry plugin for Helm.

### Install

``` shell
helm plugin install https://github.com/pho-enix/helm-quay

# On first use it downloads required assets

$ helm quay --help
Registry plugin assets do not exist, download them now !
downloading https://github.com/app-registry/appr-cli/releases/download/v0.4.1/cnr-linux-x64 ...
```


### Upgrade

##### Upgrade the appr binary

``` shell
$ helm quay list-plugin-versions
$ helm quay upgrade-plugin VERSION
downloading https://github.com/app-registry/appr-cli/releases/download/v0.4.1/cnr-linux-x64 ...
```

##### Upgrade the helm plugin

``` shell
$ cd ~/.helm/plugins/registry
$ git pull origin master
$ helm quay upgrade-plugin
downloading https://github.com/app-registry/appr-cli/releases/download/v0.4.1/cnr-linux-x64 ...
```

## Deploy Jenkins Using Helm from the Quay Registry


```
helm quay version quay.io
```

Output should be:
```
Api-version: {u'cnr-api': u'0.X.Y'}
Client-version: 0.X.Y
```

### Install Jenkins

```
helm init
helm quay list quay.io
helm quay install quay.io/charts/jenkins
```

## Create and Push Your Own Chart

First, create an account on https://quay.io and login to the CLI using the username and password

Set an environment for the username created at Quay to use through the rest of these instructions.

```
export USERNAME=philips
```

Login to Quay with the helm quay plugin:

```
helm quay login -u $USERNAME quay.io
```

Create a new Helm chart, the default will create a sample nginx application:

```
helm create nginx
```

Push this new chart to Quay and then deploy it from Quay.

```
cd nginx
helm quay push --namespace $USERNAME quay.io
helm quay install quay.io/$USERNAME/nginx
```
