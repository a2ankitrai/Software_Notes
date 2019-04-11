# Consolidating the installation of libraries and and other features in script

```

npm install --save  bootstrap@latest

npm install --save jquery@latest

npm install --save popper.js@latest

npm install --save rxjs@latest


npm install --save bootstrap@latest jquery@latest popper.js@latest rxjs@latest

```

angular core might not be coming preinstalled in v7

below command to install the same
```
npm install --save @angular/core
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
----

## Updating angular application to latest version

```
ng update @angular/cli @angular/core

```

## Errors and Resolutions

##  1

```
ERROR in node_modules/@angular/core/src/render3/ng_dev_mode.d.ts(9,11): error TS2451: Cannot redeclare block-scoped variable 'ngDevMode'.
../feature-tests/bootstrap-widget/node_modules/@angular/core/src/render3/ng_dev_mode.d.ts(9,11): error TS2451: Cannot redeclare block-scoped variable 'ngDevMode'.
```
add the following to the compilerOptions in the` tsconfig.json` file in the root of my project:
```
"paths": {
 "@angular/*": ["node_modules/@angular/*"]
}
```









---
