# Entur - CircleCI Helm Orb
This orb tries to simply huge CircleCI configuration files by adding common Helm functionality.

https://circleci.com/orbs/registry/orb/entur/helm

## Requirements
An executor that has `curl` and `gcloud` pre-installed.

## Usage

Import the orb and give it a name. Add this to the `orbs`-key in your CircleCI-configuration:
```yaml
orbs:
 helm: entur/helm@volatile 
 # volatile selects the newest version. More examples of versioning here: https://circleci.com/docs/2.0/creating-orbs/#semantic-versioning-in-orbs
```

Use the orb like this:

```yaml
jobs:
  your-job-name:
    steps:
     - helm/install-helm-chart:
         chart: Chart.yaml
         namespace: development
         release-name: my-release
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

A dev-orb will be published as: `entur/helm@dev:YOUR-BRANCH-NAME`. Release orbs are created on push to the master branch. 

You can read more here: https://circleci.com/docs/2.0/creating-orbs/