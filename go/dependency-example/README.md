# Go vendor support

## Add dependencies

```bash
$ glide init --non-interactive
$ glide get "github.com/golang/example/stringutil"
$ glide install -v
```

## Archive files
```bash
$ tree -L 1.
.
├── README.md
├── glide.lock
├── glide.yaml
├── main.go
└── vendor

$ zip -r example.zip ./*
```

## Create env with builder image

```bash
$ fission env create --name go --image fission/go-env:0.12.0 --builder fission/go-builder:0.12.0
```

## Create package
```bash
$ fission pkg create --src example.zip --env go
$ fission pkg info --name <pkg-name>
```

## Create function

* entrypoint: `<handler-function-name>`

```bash
$ fission fn create --name <fn-name> --env go --pkg <pkg-name> --entrypoint "Handler"
$ fission fn test --name <fn-name>
```
