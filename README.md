# Piwik for OpenShift 3

This repository contains an OpenShift 3 template to easily deploy Piwik on OpenShift.
With this template it's possible to run your own Piwik instance f.e. on [APPUiO](https://appuio.ch/).

## Installation

### 1 Deploy Database

```
oc -n openshift process mariadb-persistent -p MYSQL_DATABASE=piwik | oc -n MYNAMESPACE create -f -
```

### 2 Deploy Piwik

```
oc process -f https://raw.githubusercontent.com/tobru/piwik-openshift/master/piwik.yaml -p PIWIK_HOST=stats.example.com | oc -n MYNAMESPACE create -f -
```

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
