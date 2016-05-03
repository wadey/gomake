gomake
======

gomake provides a generic Makefile for Go projects.

Provides a few nice features such as:

- default `make all` target builds all binaries.
- `make cover-xml` to generate a Jenkins compatible coverage file that merges
  coverage for all packages together.
- `make dev` to run main and auto-restart the binary when sources are changed.

Works for projects that follow:

 - `bin/<repo name>` built from the root package (if it is 'main').
 - `bin/<name>` for each package `cmd/<name>`.

to use, set your Makefile to:

    GO=$(firstword $(subst :, ,$(GOPATH)))
    INSTALL_GOMAKE=$(shell go get -v github.com/wadey/gomake)
    include $(GO)/src/github.com/wadey/gomake/Makefile.in

if the project needs to run a target before the binaries are built,
override `PREBUILD`:

    GO=$(firstword $(subst :, ,$(GOPATH)))
    INSTALL_GOMAKE=$(shell go get -v github.com/wadey/gomake)

    PREBUILD=run-script
    include $(GO)/src/github.com/wadey/gomake/Makefile.in

    run-script:
        …
