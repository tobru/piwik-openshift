# Piwik for OpenShift 3

This repository contains an OpenShift 3 template to easily deploy Piwik on OpenShift.
With this template it's possible to run your own Piwik instance f.e. on [APPUiO](https://appuio.ch/).

## Installation

### 0 Create OpenShift project

Create an OpenShift project if not already provided by the service

```
PROJECT=piwik
oc new-project $PROJECT
```

### 1 Deploy Database

```
oc -n openshift process mariadb-persistent -p MYSQL_DATABASE=piwik | oc -n $PROJECT create -f -
```

### 2 Deploy Piwik

```
oc process -f https://raw.githubusercontent.com/tobru/piwik-openshift/master/piwik.yaml -p APP_URL=stats.example.com | oc -n $PROJECT create -f -
```

### 3 Configure Piwik

* Navigate to http://stats.example.com
* Fill in the form and finish the installation. The DB credentials can be 
  found in the secret `mariadb`. In the Webconsole it can be found under
  `Resources -> Secrets -> mariadb -> Reveal Secret`

**Hints**

* You might want to enable TLS for your instance

#### Template parameters

Execute the following command to get the available parameters:

```
oc process -f https://raw.githubusercontent.com/tobru/piwik-openshift/master/piwik.yaml --parameters
```

## Contributions

Very welcome!

1. Fork it (https://github.com/tobru/piwik-openshift/fork)
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
