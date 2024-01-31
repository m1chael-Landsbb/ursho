# crdvalidate
`crdvalidate` is a CLI tool for analyzing Kubernetes `CustomResourceDefinition` resources (CRDs) for schema differences.
It detects incompatible modifications to assist:
- Cluster administrators in safeguarding CRDs from disruptive changes
- GitOps practitioners in preventing CRDs with breaking changes from being merged
- Developers of Kubernetes extensions in identifying when CRD modifications introduce incompatibilities

## Usage
```sh
crdvalidate is a tool for assessing modifications to Kubernetes CustomResourceDefinitions
to assist cluster administrators, gitops practitioners, and Kubernetes extension developers in identifying
modifications that could negatively impact clusters and/or users.

Example use cases:
    Assessing a modification in a CustomResourceDefinition on a Kubernetes Cluster against one in a file:
        $ crdvalidate kube://{crd-name} file://{filepath}

    Assessing a modification from file to file:
        $ crdvalidate file://{filepath} file://{filepath}

    Assessing a modification from git ref to git ref:
            $ crdvalidate git://{ref}?path={filepath} git://{ref}?path={filepath}

Usage:
  crdvalidate <old> <new> [flags]
  crdvalidate [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  help        Help about any command
  version     installed version of crdvalidate

Flags:
      --config string   the filepath to load the check configurations from
  -h, --help            help for crdvalidate
  -o, --output string   the format the output should take when incompatibilities are identified. May be one of plaintext, json, yaml (default "plaintext")

Use "crdvalidate [command] --help" for more information about a command.
```

The `<old>` and `<new>` arguments are required and should be the sourcing information for the old and new
`CustomResourceDefinition` YAML

The supported sources are:
- `kube://{name}`
- `git://{ref}?path={filepath}`
- `file://{filepath}`

An example of using `crdvalidate` to compare a `CustomResourceDefinition` on a Kubernetes cluster to the same one in a local file:
```sh
crdvalidate kube://memcacheds.cache.example.com file://crd.yaml
```

## Installation

`crdvalidate` can be installed by running:
```sh
go install sigs.k8s.io/crdvalidate@{revision}
```

Replace `{revision}` with a tag, commit, or `latest` to build and install the tool from source at that particular revision.
