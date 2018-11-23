## Solidity "AssertionError [ERR_ASSERTION]: Invalid callback specified" errors

Solidity released version 0.5.0 and introduced many breaking changes. This particular version is VERY unstable at the moment.

When running your test code you are probably getting or will probably get the following:

```
AssertionError [ERR_ASSERTION]: Invalid callback specified
```

If so, you should:

1. Uninstall solc:
```
npm uninstall solc
```

2. Reinstall one of two versions:

The version used in the course:
```
npm install --save solc@0.4.17
```
or

The newest version that will not break:
```
npm install --save solc@0.4.25
```
