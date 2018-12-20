# Real-time User Stories Demo


This repository contains the code used to demo building feature branches from Github with AWS Codebuild and deploying onto AWS Fargate.


## Codebuild Project


To create the Codebuild project:

Github:
```
$ aws cloudformation create-stack --stack-name real-time-user-stories-codebuild --template-body file://codebuild.yml --parameters \
ParameterKey=RepositoryType,ParameterValue=GITHUB \
ParameterKey=RepositoryLocation,ParameterValue=https://github.com/rslotte/real-time-user-stories-demo.git \
--capabilities CAPABILITY_NAMED_IAM
```

Bitbucket:
```
$ aws cloudformation create-stack --stack-name real-time-user-stories-codebuild --template-body file://codebuild.yml --parameters \
ParameterKey=RepositoryType,ParameterValue=BITBUCKET \
ParameterKey=RepositoryLocation,ParameterValue=https://bitbucket.org/rslotte-contino/real-time-user-stories-demo.git \
--capabilities CAPABILITY_NAMED_IAM
```

Modify the trigger if you only want to build on a specific branch naming pattern:
```
$ aws codebuild update-webhook --project-name real-time-user-stories-codebuild --branch-filter ^story\\d+$
```

## Feature branches on Fargate

See `buildspec.yml`
