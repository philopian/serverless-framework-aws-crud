# What is this?
- Expressjs RESTful application with AWS locally
- *Note:* Every time you close the connection the DB will loose all it's data

# Local development
- Install some global packages
  ```shell
  $ npm install -g serverless serverless-dynamodb-local serverless-offline

  # Init a new application
  $ serverless
  ```

1. Configure your DynamoDB client
  ```js
  const dynamoDbClientParams = {};
  if (process.env.IS_OFFLINE) {
    AWS.config.update({
      region: "us-west-2",
      accessKeyId: "accessKeyId",
      secretAccessKey: "secretAccessKey",
    });

    dynamoDbClientParams.region = "localhost";
    dynamoDbClientParams.endpoint = "http://localhost:8000";
  }
  const dynamoDbClient = new AWS.DynamoDB.DocumentClient(dynamoDbClientParams);
  ```

2. Update the `serverless.yml` file with offline config
```yml
custom:
  tableName: 'users-table-${sls:stage}'
  dynamodb:
    stages:
      - dev
    start:
      - migrate: true
  serverless-offline:
    resourceRoutes: true # HTTP proxy lambdas

plugins:
  - serverless-dynamodb-local
  - serverless-offline
```

3. Install serverless local dynamodb
  ```shell
  $ sls dynamodb install
  ```

4. Run the serverless framework locally
  ```shell
  $ sls offline start
  ```








