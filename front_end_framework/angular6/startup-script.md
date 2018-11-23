# Consolidating the installation of libraries and and other features in script

```

npm install --save  bootstrap@latest

npm install --save jquery@latest

npm install --save popper.js@latest


```


Add the file paths for the libraries installed in angular.json file

```
"styles": [
  "node_modules/bootstrap/dist/css/bootstrap.min.css",
  "src/styles.css"
],
"scripts": [
  "node_modules/jquery/dist/jquery.min.js",
  "node_modules/bootstrap/dist/js/bootstrap.bundle.min.js"
]
```

## Installing ng-bootstrap library

```
npm install --save @ng-bootstrap/ng-bootstrap
```

angular core might not be coming preinstalled in v7

below command to install the same
```
npm install --save @angular/core
```


----

## Updating angular application to latest version

```
ng update @angular/cli @angular/core

```










---
