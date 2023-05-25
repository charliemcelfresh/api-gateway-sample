## sam-app

### Build and Run

`make build`

All your binaries will end up in this app, in the `.aws-sam/build` folder.

This is because the template.yaml files for those applications are referred to in the template.yaml file at the base of this app.

In shared envs, instead of referring to local file paths, we'll
* build each app separately, and push each to S3
* grab their arns, and refer to each arn in our template.yaml

run `make start-api`

Then hit

`http:localhost:3000/hello` and `http:localhost:3000/goodbye`