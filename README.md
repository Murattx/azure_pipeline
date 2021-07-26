# Introduction 
This repository has the shared Azure CI pipeline Library
# Usage
Below are the steps to use shared pipeline.
+ Copy the sample pipeline 
+ Change the CI trigger and PR trigger branches accordingly
+ Change the DEV and QA branches

### Sample Template
```
--- 
trigger: 
  branches: 
    include: 
      - master
      - releases/*
      - develop
pr: 
  branches: 
    include: 
      - main
      - releases/*
      - develop
resources:
  repositories:
    - repository: pipeline
      type: git
      name: "Mobile API v1/ci-common-pipeline"
      
variables: 
  - template: variables.yml@pipeline
stages:
- template: build.yml@pipeline
  parameters:
    publish:   [
        { "branchName" :"refs/heads/develop", "env":"dev"}, 
        { "branchName" :"refs/heads/releases/v1", "env":"qa"} 
     ]
```