# Matomo (was: Piwik) for OpenShift 3

This repository contains an OpenShift 3 template to easily deploy [Matomo](https://matomo.org/)
on OpenShift. With this template it's possible to run your own Matomo
instance f.e. on [APPUiO](https://appuio.ch/).

*Note*: [Piwik has been renamed into Matomo](https://matomo.org/blog/2018/01/piwik-is-now-matomo/)
in early 2018. Some names still refer to Piwik and probably won't be changed
soon or easily (like this repository or the official Docker image on
[Docker Hub](https://hub.docker.com/_/piwik/). This can be confusing from
time to time.

## Installation

### 0 Create OpenShift project

Create an OpenShift project if not already provided by the service

```
PROJECT=matomo
oc new-project $PROJECT
```

### 1 Deploy Database

```
oc -n openshift process mariadb-persistent -p MYSQL_DATABASE=matomo | oc -n $PROJECT create -f -
```

### 2 Deploy Matomo

```
oc process -f https://raw.githubusercontent.com/tobru/piwik-openshift/master/matomo.yaml -p APP_URL=stats.example.com | oc -n $PROJECT create -f -
```

### 3 Configure Matomo

* Navigate to http://stats.example.com
* Fill in the form and finish the installation. The DB credentials can be 
  found in the secret `mariadb`. In the Webconsole it can be found under
  `Resources -> Secrets -> mariadb -> Reveal Secret`

**Hints**

* You might want to enable TLS for your instance

#### Template parameters

Execute the following command to get the available parameters:

```
oc process -f https://raw.githubusercontent.com/tobru/piwik-openshift/master/matomo.yaml --parameters
```

## Contributions

Very welcome!

1. Fork it (https://github.com/tobru/piwik-openshift/fork)
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
