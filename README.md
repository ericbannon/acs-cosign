# Overview 

GitHub action for cosigning images

## Instructions

### Download cosign

Go to the GitHub repo for sigstore/cosign, click on Releases, and download the version for your operative system.

### Generate secrets for GitHub action including keypair

``` 
export GITHUB_TOKEN=ghp_xyz123

export COSIGN_PASSWORD=pwd123

./cosign generate-key-pair github://<your-repo>/<sub-path>
```

You should now see 3 secrets saved under your GitHub actions settings in the repository. These will be used later for signing images as part of the CI build. 


