# Serverless Stack Demo API

[Serverless Stack](http://serverless-stack.com) is a free comprehensive guide to creating full-stack serverless applications. We create a [note taking app](http://demo.serverless-stack.com) from scratch.

This repo is for the serverless backend API that we build over the course of the tutorial. You can find the repo for the frontend React app [here](https://github.com/AnomalyInnovations/serverless-stack-demo-client). And the repo for the tutorial [here](https://github.com/AnomalyInnovations/serverless-stack-com).

#### Steps

To support the different chapters and steps of the tutorial; we use branches to represent the project codebase at the various points. Here is an index of the various chapters and branches in order.

- [Set up the Serverless Framework](../../tree/setup-the-serverless-framework)
- [Add Support for ES6/ES7 JavaScript](../../tree/add-support-for-es6-es7-javascript)
- [Add a Create Note API](../../tree/add-a-create-note-api)
- [Add a Get Note API](../../tree/add-a-get-note-api)
- [Add a List All the Notes API](../../tree/add-a-list-all-the-notes-api)
- [Add an Update Note API](../../tree/add-an-update-note-api)
- [Add a Delete Note API](../../tree/add-a-delete-note-api)

#### Usage

To use this repo locally you need to have the [Serverless framework](https://serverless.com) installed.

``` bash
$ npm install serverless -g
```

Clone this repo and install the NPM packages.

``` bash
$ git clone https://github.com/AnomalyInnovations/serverless-stack-demo-api
$ npm install
```

Run a single API on local.

``` bash
$ serverless invoke local --function list --path event.json
```

Where, `event.json` contains the request event info and looks something like this.

``` json
{
  "requestContext": {
    "authorizer": {
      "claims": {
        "sub": "USER-SUB-1234"
      }
    }
  }
}
```

Finally, run this to deploy to your AWS account.

``` bash
$ serverless deploy
```

#### Maintainers

Serverless Stack is authored and maintained by Frank Wang ([@fanjiewang](https://twitter.com/fanjiewang)) & Jay V ([@jayair](https://twitter.com/jayair)). [**Subscribe to our newsletter**](http://eepurl.com/cEaBlf) for updates on Serverless Stack. Send us an [email][Email] if you have any questions.

[Email]: mailto:contact@anoma.ly

#### Tests

[Simple API tests](https://serverless-stack.com/chapters/test-the-configured-apis.html)

Create a user.

```sh
$ aws cognito-idp sign-up \
  --region YOUR_DEV_COGNITO_REGION \
  --client-id YOUR_DEV_COGNITO_APP_CLIENT_ID \
  --username admin@example.com \
  --password Passw0rd!
```

Confirm a user.

```sh
$ aws cognito-idp admin-confirm-sign-up \
  --region YOUR_DEV_COGNITO_REGION \
  --user-pool-id YOUR_DEV_COGNITO_USER_POOL_ID \
  --username admin@example.com
```

Post a note.

```sh
$ npx aws-api-gateway-cli-test \
--username='admin@example.com' \
--password='Passw0rd!' \
--user-pool-id='YOUR_DEV_COGNITO_USER_POOL_ID' \
--app-client-id='YOUR_DEV_COGNITO_APP_CLIENT_ID' \
--cognito-region='YOUR_DEV_COGNITO_REGION' \
--identity-pool-id='YOUR_DEV_IDENTITY_POOL_ID' \
--invoke-url='YOUR_DEV_API_GATEWAY_URL' \
--api-gateway-region='YOUR_DEV_API_GATEWAY_REGION' \
--path-template='/notes' \
--method='POST' \
--body='{"content":"hello world","attachment":"hello.jpg"}'
```
