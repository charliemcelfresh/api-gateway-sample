## api-gateway-sample

This is a proof-of-concept that creates separate Go binaries for two applications: `hello-world` and `goodbye-world`.

The idea here is that we can create as many separate Go applications as we need, and run them all under one AWS API Gateway.

Locally, we run these applications using [AWS SAM](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-local-start-api.html)

Running SAM locally is not 1:1 with running an API Gateway in AWS, but the ideas are similar.

Locally:

* We have one template.yaml file at the base of the app, that refers to each binary's template.yaml file in api-gateway/.aws-sam/build/<*>WorldFunction/template.yaml
* The build command below will build both binaries

Remotely, the idea is to build each binary separately, push it to S3, and, rather than pointing to our local template.yaml files, instead refer to each binary's arn.

### Build and Run

`cd api-gateway && make build`

This will create  `api-gateway/.aws-sam/build` folder.

The template.yaml files for those applications are referred to in the template.yaml file at the base of this app.

In shared envs, instead of referring to local file paths, we'll
* build each app separately, and push each to S3
* grab their arns, and refer to each arn in our template.yaml

run `make start-api`

Then hit

`http:localhost:3000/hello` and `http:localhost:3000/goodbye`