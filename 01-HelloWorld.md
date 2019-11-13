# Overview

[TERRA](https://app.terra.bio/) is used to run workflows (and notebooks) on Google Cloud. It uses [WDL](https://software.broadinstitute.org/wdl/) as it's workflow script (instead of e.g. [NextFlow](https://www.nextflow.io/)).

Workflow's cannot be edited directly on TERRA. They have to be created locally (or on HPC) then pushed to github, imported into dockstore and then into TERRA. There's probably other ways of doing it but this guide explains how to do it this way.

# Related resources

* [Lynn Langit's tutorials](https://github.com/lynnlangit/gcp-for-bioinformatics).

# Tutorial

1. Set up cromwell on local computer following [this guide](https://cromwell.readthedocs.io/en/stable/tutorials/FiveMinuteIntro/)
* The guide explains how to install cromwell, create a basic workflow and run it locally

2. Create a github account if you don't have one already
* Then create a repository
* In the folder you used for the cromwell, and where your workflow script ('myWorkflow.wdl') is located, create a github repository using the instructions shown on github when you create a repo
* Add your workflow script to the repository and push to the repo

```
git add myWorkflow.wdl
git commit -m "added basic workflow script"
git push origin master
```

3. Go to [dockstore](https://dockstore.org/) and login using your github account
* You will also need to link your google account so that you can login to TERRA. This is done through the [onboarding page](https://dockstore.org/onboarding)
* Follow instructions on the onboarding page for installing Java 11, Docker and Dockerstore command line program

4. Add your repository from github onto dockstore:
* Click on your login name in top right corner of dockstore. Select 'My Workflows'
* Click 'Register Workflow'
* A popup window comes up. Select "Use CWL, WDL or Nextflow from GitHub, Bitbucket, etc" then press "Next"
* Under 'source code repository' enter the location of your repo that contains your workflow file. For instance, I added "neurogenomics/WDLtest"
* Select 'WDL'
* Under 'Workflow Path' enter the location of the workflow file. In my github repo it is in the root folder, so it is "/myWorkflow.wdl"
* I did not create a test parameter file path
* In the resulting page, click 'Publish'

# Things which should be added in the next tutorial

* Test parameter files
* Using Combiz's single cell docker file on Imperial's cluster and on TERRA
* Editing Combiz's single cell docker file

# Brief explanation of some terms/names you may encounter

* Quay.io. This is the repository that dockstore recommends to use for storing docker images. Note that docker images are not the same as the docker build scripts. The scripts will be stored on github. Once they are built they are large files which get stored on quay.io.
* DockerHub. Another repository used for storing docker images.