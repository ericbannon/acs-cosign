# Overview 

A simple GitHub action example for cosigning images in authenticated Quay registries (Note: can be modified with any OCI compliant registry by adjusting the docker login task under the github action). 

## Instructions

### Download cosign

Go to the GitHub repo for sigstore/cosign, click on Releases, and download the version for your operative system.

### Generate secrets for GitHub action including keypair

Generate a GitHub PAT with write access to the repo 

``` 
export GITHUB_TOKEN=ghp_xyz123

export COSIGN_PASSWORD=pwd123

./cosign generate-key-pair github://<your-repo>/<sub-path>
```

You should now see 3 secrets saved under your GitHub actions settings in the repository. These will be used later for signing images as part of the CI build. 

### Specify the image that you want to sign 



