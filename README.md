



```shell
$ npm install -g serverless serverless-dynamodb-local serverless-offline

$ serverless
```

- Make bogass credentials `~/.aws/credentials`
  ```shell
  aws_access_key_id = aws_access_key_id
  aws_secret_access_key = aws_secret_access_key
  ```
- configure your DynamoDB client
  ```js
  const dynamoDbClient = new AWS.DynamoDB.DocumentClient({
    region: "us-west-2",
    accessKeyId: "aws_access_key_id",
    secretAccessKeyId: "aws_secret_access_key",
    endpoint: "https://localhost:8000",
  });
  ```
