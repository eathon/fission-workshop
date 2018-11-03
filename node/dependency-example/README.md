# Node npm support

## Add dependencies

Write `package.json`

```bash
{
  "name": "fission-nodejs-runtime",
  "engines": {
    "node": ">=7.6.0"
  },
  "dependencies": {
    "moment": "*"
  }
}
```

## Archive files
```bash
$ tree -L 1.
.
├── README.md
├── momentExample.js
└── package.json

$ zip -r example.zip ./*
```

## Create env with builder image

```bash
$ fission env create --name node --image fission/node-env:0.12.0 --builder fission/node-builder:0.12.0
```

## Create package
```bash
$ fission pkg create --src example.zip --env nodejs
$ fission pkg info --name <pkg-name>
```

## Create function

* entrypoint: `<filename>`. 
    * If the file name is `momentExample.js`, then the entrypoint is `momentExample`.
    * If there are multiple exports like following, the entrypoint is `momentExample.entry1`(`<filename>.<export-name>`).
      
```javascript
module.exports.entry1 = async function(context) {
    return {
        status: 200,
        body: "Hello, entry 1!\n"
    };
}

module.exports.entry2 = async function(context) {
    return {
        status: 200,
        body: "Hello, entry 2!\n"
    };
}
``` 

```bash
$ fission fn create --name <fn-name> --env nodejs --pkg <pkg-name> --entrypoint "momentExample"
$ fission fn test --name <fn-name>
```
