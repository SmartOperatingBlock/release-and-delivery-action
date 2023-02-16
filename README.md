# Release and delivery action
![Release](https://github.com/smartoperatingblock/release-and-delivery-action/actions/workflows/release.yml/badge.svg)

A simple composite GitHub Action taking care of the release and the docker container delivery of a project.

## Usage
The objective of the action is to be able to perform the release and the delivery of a software artifact.
For this reason, when you want to perform both of them we force to have the same version on both the release and
the container image tag.
So, when you want to perform the release, in order to be able to build and deliver the container you need 
to set the `CONTAINER_VERSION` GitHub environment variable corresponding to the current version released.

If you perform the release you can specify it within the release command as shown below.
Otherwise, if you do not perform release but only container delivery
then specify it as *env* inside the step or job or workflow.

If you don't perform the release then you can also avoid to specify the `CONTAINER_VERSION` and only
the *latest* tag will be used.

``` yaml
- uses: SmartOperatingBlock/release-and-delivery-action@<latest-version>
  with:
    # True if the action should perform the release of the project
    # Default: true
    should-release: true/false
  
    # The command executed to perform the release
    release-command: |
      <command(s) to perform in order to release>
      echo "CONTAINER_VERSION=<your new version>" >> $GITHUB_ENV # Also as command after release
    
    # True if the action should perform the build and the delivery 
    # of the docker image of the project
    # Default: true
    should-build-and-deliver-container: true/false

    # The Dockerfile file path to use
    # Default: 'Dockerfile'
    docker-file-src: 'subfolder/Dockerfile'

    # Server address of the container registry. 
    # If not set then will default to Docker Hub
    container-registry-name: ''

    # Username used to log against the container registry
    container-registry-username: '<username>'

    # Password or personal access token used to log against the container registry
    container-registry-password: '<password>'

    # The name of docker container image to build and deliver
    # Default: '${{ github.repository }}'
    image-name: '<image name>'
    
    # The GitHub token, it will be exposed in the release step
    # as the environment variable GITHUB_TOKEN
    github-token: '<token>'

```

# License
The scripts in this project are released under the [MIT License](LICENSE)