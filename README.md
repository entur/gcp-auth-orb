# Entur - CircleCI GCP Authentication Orb

> This is a work in progress, not yet available as a pulic release.

This orb is a utility orb for other orbs to easily authenticate with GCP

https://circleci.com/orbs/registry/orb/entur/gcp-auth

## Requirements
An executor that has `gcloud` pre-installed. One is available as gcp-auth/entur-cci-toolbox

## Usage

Import the orb and give it a name. Add this to the `orbs`-key in your CircleCI-configuration:
```yaml
orbs:
 gcp-auth: entur/gcp-auth@volatile 
 # volatile selects the newest version. More examples of versioning here: https://circleci.com/docs/2.0/creating-orbs/#semantic-versioning-in-orbs
```

Use the orb like this:

```yaml
jobs:
  your-job-name:
    steps:
     - gcp-auth/authenticate-gcp:
          name: use-gcloud-cli-for-something
          context: context-with-appropriate-gcp-credentials # You can add the gcp-service-key & gcp-container-cluster in the context.
     # do more CircleCI stuff.
``` 
         
Available commands can be found in `src/commands`. Usage examples in `examples`             

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