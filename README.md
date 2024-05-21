# This workflow pics file from local repo and pushes it to azure storage.

name: azure file upload

on:
  push:
    branches:
      - main

jobs:  

  upload-iles-in-dev:
    runs-on : ubuntu-latest
    steps:

    - name: Checkout
      uses: actions/checkout@v3
        

    - name: Azure Login
      uses: azure/login@v2
      with:
        creds: ${{ secrets.AZURE_CREDENTIALS }}


    - name: Azure storage file upload
      uses: azure/cli@v1
      with:
        azcliversion: latest
        inlineScript: |
           az storage blob upload-batch --account-name rg1 --destination dev --destination-path https://rg1.blob.core.windows.net/dev --source .github/workflows
