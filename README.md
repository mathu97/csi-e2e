Introduction
============

This repository contains the Kubernetes E2E test framework set up in
such a way that it runs the Kubernetes volume tests for the
example `hostpath` driver.

Usage
=====

No cloud-specific code gets imported, so tests can only be run against
a cluster that has already been set up. Set the the usual
`KUBECONFIG=<config file>` and then run `go test -v ./test/e2e` or
`ginkgo ./test/e2e`.

Adding `-provider=local` suppresses a message about the flag not being
set and treating the run as "conformance test", but has no other
effect in practice.

The
[upstream documentation](https://github.com/kubernetes/community/blob/master/contributors/devel/e2e-tests.md#local-clusters)
uses `hack/e2e.go` as wrapper around the test execution. This is not
necessary for the test suite defined in this repository.

Adding Tests
============

New tests can be written in their own packages under `test/e2e` and
then need to be added to the import list in `test/e2e_test.go`.

Running Tests Locally
=====================

* Launch a local kube cluster: `ALLOW_PRIVILEGED=1 hack/local-up-cluster.sh` 

In a seperate shell:
* Set KubeConfig environment variable: `export KUBECONFIG=<config file>`
* A JSON config file like [this](https://github.com/mathu97/csi-e2e/blob/master/test/e2e/driver_manifest.json) is required for the tests to run. 
* Create an environment variable named `DRIVER_MANIFEST` that has the path to your JSON config file (`export DRIVER_MANIFEST=driver_manifest.json` to run e2e tests on hostpath CSI driver)
* Run tests: `go test -v ./test/e2e` (might need to turn GOCACHE off sometimes `GOCACHE=off go test -v ./test/e2e`)
