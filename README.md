# Overview 

A simple GitHub action example for cosigning images in authenticated Quay registries (Note: can be modified with any OCI compliant registry by adjusting the docker login task under the github action). The action works by taking the input from the IMAGE file and running the cosign installer, proceeded by the signing of the image and pushing of signature to the registry. 

## Instructions

### Download cosign

Go to the GitHub repo for sigstore/cosign, click on Releases, and download the version for your operative system.

### Generate secrets for GitHub action including cosign keypair

Option 1: Generate cosign keypair and password secrets directly to github

Generate a GitHub PAT with write access to the repo 

``` 
export GITHUB_TOKEN=ghp_xyz123

export COSIGN_PASSWORD=pwd123

./cosign generate-key-pair github://<your-repo>/<sub-path>
```

Option 2: Manually create the following action secrets after generating keypair locally:
1. COSIGN_PASSWORD
2. COSIGN_PRIVATE_KEY
3. COSIGN_PUBLIC_KEY

Next, generate secrets for you Quay registry (or replace this in the code with you own env variable): 
1. QUAY_USERNAME
2. QUAY_PASSWORD

You should now see 5 secrets saved under your GitHub actions settings in the repository. These will be used later for signing images as part of the CI build. 

### Specify the image that you want to sign

Modify the IMAGE file with the image in your registry you want to sign and push to the main branch to kick off the CI build. Note: This could be done in a PR for review purposes of an image signing request from the end user in the chain of custody for the image. 


## OPTIONAL (Add an ACS Image Check for Policy Violations)

Step 1: Create a secret called CENTRAL, where this is your central endpoint (minus port)
Step 2: Create a secret called ROX_API_TOKEN, where this is an API token generated from Central
