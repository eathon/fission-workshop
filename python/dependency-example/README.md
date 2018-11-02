# Python pip support

## Add dependencies

Write `requirements.txt` & create `__init__.py`

```bash
pyyaml
```

## Archive files
```bash
$ tree -L 1.
.
├── README.md
├── __init__.py
├── requirements.txt
└── user.py


$ zip -r example.zip ./*
```

## Create package
```bash
$ fission pkg create --src example.zip --env python
$ fission pkg info --name <pkg-name>
```

## Create function

* entrypoint: `<file>.<def-name>`

```bash
$ fission fn create --name <fn-name> --env python --pkg <pkg-name> --entrypoint "user.main"
$ fission fn test --name <fn-name>
```
