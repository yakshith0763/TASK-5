Create a buildspec.yml File:

phases:
  install:
    runtime-versions:
      java: corretto11
  pre_build:
    commands:
      - echo Logging in to Amazon ECR...
      - aws --version
      - $(aws ecr get-login --no-include-email --region $AWS_DEFAULT_REGION)
  build:
    commands:
      - echo Build started on `date`
      - ./mvnw clean install
  post_build:
    commands:
      - echo Build completed on `date`
      - echo Pushing the Docker image...
      - docker build -t $REPOSITORY_URI:$CODEBUILD_RESOLVED_SOURCE_VERSION .
      - docker push $REPOSITORY_URI:$CODEBUILD_RESOLVED_SOURCE_VERSION
artifacts:
  files: imagedefinitions.json
