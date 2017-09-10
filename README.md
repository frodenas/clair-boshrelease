# Clair BOSH Release

This is a [BOSH](http://bosh.io/) release for [Clair](https://github.com/coreos/clair), an open source project for the [static analysis](https://en.wikipedia.org/wiki/Static_program_analysis) of vulnerabilities in application containers.

## Table of Contents

* [Usage](https://github.com/frodenas/clair-boshrelease#usage)
  * [Requirements](https://github.com/frodenas/clair-boshrelease#requirements)
  * [Clone the repository](https://github.com/frodenas/clair-boshrelease#clone-the-repository)
  * [Basic deployment](https://github.com/frodenas/clair-boshrelease#basic-deployment)
  * [Operations files](https://github.com/frodenas/clair-boshrelease#operations-files)
  * [Deployment variables and the var-store](https://github.com/frodenas/clair-boshrelease#deployment-variables-and-the-var-store)
* [Contributing](https://github.com/frodenas/clair-boshrelease#contributing)
* [License](https://github.com/frodenas/clair-boshrelease#license)

## Usage

### Requirements

In order to use this BOSH release you will need:

* [BOSH CLI v2](https://bosh.io/docs/cli-v2.html)
* An already deployed [BOSH environment](http://bosh.io/docs/init.html)
* A compatible [cloud-config](http://bosh.io/docs/terminology.html#cloud-config) with a `default` option for `network` and `vm_types` (you can use the example that comes from [cf-deployment](https://github.com/cloudfoundry/cf-deployment/blob/master/bosh-lite/cloud-config.yml))

###  Clone the repository

First, clone this repository into your workspace:

```
git clone https://github.com/frodenas/clair-boshrelease
cd clair-boshrelease
export BOSH_ENVIRONMENT=<name>
```

### Basic deployment

To deploy a basic `clair` server use the following command:

```
bosh -d clair deploy manifests/clair.yml \
  --vars-store tmp/deployment-vars.yml
```

### Operations files

Additional [operations files](http://bosh.io/docs/cli-ops-files.html) are located at the [manifests/operators](https://github.com/frodenas/clair-boshrelease/tree/master/manifests/operators) directory. Those files includes a basic configuration, so extra ops files might be needed for additional configuration.

Please review the op files before deploying them to check the requeriments, dependencies and necessary variables.

| File | Description | exporter | dashboards | alerts |
| ---- | ----------- |:--------:|:----------:|:------:|

### Deployment variables and the var-store

Some operators files requires additional information to provide environment-specific or sensitive configuration such as various credentials. To do this in the default configuration, we use the `--vars-store`. This flag takes the name of a `yml` file that it will read and write to. Where necessary credential values are not present, it will generate new values based on the type information stored at the different deployment files. Necessary variables that BOSH can't generate need to be supplied as well.
See each particular op files you're using for any additional necessary variables.

See also the [BOSH CLI documentation](http://bosh.io/docs/cli-int.html#value-sources) for more information about ways to supply such additional variables.

## Contributing

Refer to [CONTRIBUTING.md](https://github.com/frodenas/clair-boshrelease/blob/master/CONTRIBUTING.md).

## License

Apache License 2.0, see [LICENSE](https://github.com/frodenas/clair-boshrelease/blob/master/LICENSE).
