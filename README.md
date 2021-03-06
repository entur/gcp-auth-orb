# Entur - CircleCI GCP Authentication Orb [![CircleCI](https://circleci.com/gh/entur/gcp-auth-orb/tree/master.svg?style=svg)](https://circleci.com/gh/entur/gcp-auth-orb/tree/master)

This orb is a utility orb for other orbs to easily authenticate with GCP

https://circleci.com/orbs/registry/orb/entur/gcp-auth

## Requirements
An executor that has `gcloud` pre-installed. One is available as `gcp-auth/entur-cci-toolbox`

## Usage

Use the orb like this:

```yaml
version: 2.1

orbs: # This makes the gcp-auth orb available in your config
  gcp-auth: entur/gcp-auth@volatile # Use volatile if you always want the newest version.

executors:
  entur-cci-toolbox: gcp-auth/entur-cci-toolbox

jobs:
  do-something-with-gcloud:
    executor: entur-cci-toolbox
    steps:
      - checkout
      - gcp-auth/authenticate-gcp
      # now, do something useful
  do-something-with-kubernetes:
    executor: entur-cci-toolbox
    steps:
      - checkout
      - gcp-auth/authenticate-gcp-kubernetes
      # now, do something useful

workflows:
  version: 2.1
  main:
    jobs:
      - do-something-with-gcloud:
          context: 
            - org-devstage-dev # or maybe dev if on gh/entur
            - global #where $DOCKERHUB_LOGIN and $DOCKERHUB_PASSWORD stored
      - do-something-with-kubernetes:
          context: org-devstage-dev #or maybe dev if on gh/entur
``` 
         
Available commands can be found in `src/commands`. Usage examples in `examples` and in `text/install-test.yml`       

NB! Add $DOCKERHUB_LOGIN and $DOCKERHUB_PASSWORD credentials in your context to log in to Docker hub
## Pack and publish orb

Make sure you have the CircleCI CLI:
```bash
curl -fLSs https://circle.ci/cli | bash 
```      

Pack the contents of src/ to a single orb file:
```bash
circleci config pack ./src > orb.yml
```

Validate that the orb is valid:
```bash
circleci orb validate orb.yml
```

After commit & push to the repository, the orb will be automatically published as part of the workflow in CircleCI. 

A dev-orb will be published as: `entur/gcp-auth@dev:YOUR-BRANCH-NAME`. Release orbs are created on push to the master branch. 

You can read more here: https://circleci.com/docs/2.0/creating-orbs/
