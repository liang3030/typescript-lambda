### Init a typescript project

- Create a project folder and init project

```shell
mkdir nodejs-typescript-aws

cd nodejs--typescript-aws

npm init -y
```

- Install dependencies

```shell
npm i --save-dev typescript @types/node ts-node ts-node-dev
```

- Create configuration file. It will generate a `tsconfig.json` file.

```
npx tsc --init

```

- Update configuration file
  Open tsconfig.json file, add `rootDir` and `outDir`. rootDir is the entry point of the project. outDir is the location of bundle and build project.

"rootDir": "./src",
"outDir": "./dist"

- Add entry file `index.ts`
  Create a folder `src` in the root of project repository. Inside in the src, create a `index.ts` file. It is the entry file of the project.

- Add script for dev, build and production
  Open package.json file, inside in the `scripts`, add commands

"dev": "ts-node-dev --exit-child src/index.ts",
"build": "npx tsc",
"start": "node dist/index.js",

### Build and deploy a simple AWS lambda function

#### Deploy with command

- Install dependency

```shell
npm i --save aws-lambda
npm install -D @types/aws-lambda
```

- Add handler logic

### Deploy AWS lambda function

- Build project

remove previous build

```shell
npm run prebuild
```

build latest lambda function

```shell
npm run build
```

- Deploy or Create Lambda function with zip file

```shell
aws lambda create-function --function-name hello-world --runtime "nodejs18.x" --role arn:aws:iam::123456789012:role/lambda-ex --zip-file "fileb://dist/index.zip" --handler index.handler

```

#### Deploy with github action

<!-- TODO: the configuration is not correct at the moment -->

The action file could be find in `./github/workflows/deploy.yml`

### Create API Gateway

#### create by aws UI

1. Go to API Gateway service, click on `Create API` on the top right.
2. Select `HTTP API` and click on `Build`.
3. Choose `Lambda` in `integration`, then select `AWS Region` and `Lambda Function`.
4. Input api name, then click on `NEXT`, `NEXT` until `route` page
5. Click on `Create` on left top along with route name created in last step.
6. Select method, for example `GET`, and input the route, then click on `Create`. It will redirect to route page.
7. In the route page, select the route created by last step and attach an integration (lambda function deployed).
8. Now could test the function with API Gateway.

#### config API Gateway by IaC

TODO:

### Reference

1. [Easily deploy TypeScript project to AWS Lambda using Github Actions](https://medium.com/aspecto/easily-deploy-typescript-project-to-aws-lambda-using-github-actions-5830c1cc3997)
2.
