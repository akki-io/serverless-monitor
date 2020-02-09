<h1 align="center">
    <img src="https://raw.githubusercontent.com/akki-io/serverless-monitor/master/images/logo.png" alt="serverless-monitor" width="100"> <br>
    Serverless Monitor <br>
</h1>

<h3 align="center">
    A serverless website monitoring tool built on AWS Infrastructure.
</h3>

<img src="https://raw.githubusercontent.com/akki-io/serverless-monitor/master/images/architecture.png" alt="serverless-monitor">

## Key Features

- 100% Serverless
- Unlimited website monitoring
- Slack alerts only when status is changed
- Basic Cloudwatch Graphs and Metrics
- Docker support For development environment
- *Low cost monitoring

## Prerequisite

- [AWS Account](https://aws.amazon.com/)
- [nodeJs](https://nodejs.org/en/) OR docker with docker-compose 
- [AWS CLI](https://aws.amazon.com/cli/) OR docker with docker-compose 
- [Serverless Framework]() OR docker with docker-compose 


## Getting Started

1. Clone the repo locally
```shell script
git clone git@github.com:akki-io/serverless-monitor.git
```

### With Docker

1. Start the docker container
```shell script
docker-compose up -d
```
2. Install Dependencies
```shell script
docker-compose exec node npm install
```
3. Configure AWS CLI
```shell script
docker-compose exec node aws configure
```

### Without Docker

1. Install Dependencies
```shell script
npm install
```
2. Configure AWS CLI
```shell script
aws configure
```

### Update `serverless.yml`

Configure a slack incoming webhook and update `slackWebhookUrl`

```yaml
environment:
    stage: ${opt:stage}
    slackWebhookUrl: UPDATE_YOUR_SLACK_WEBHOOK HERE # https://slack.com/intl/en-ca/help/articles/115005265063-Incoming-Webhooks-for-Slack
```

Update your website/api urls under `input`

```yaml
input:
    - 'https://www.google.com'
    - 'https://www.tekz.io'
    - 'https://www.akki.io'
```

## Deployment

Once you have modified your `serverless.yml` it is time to deploy the project to AWS.

### With Docker

```shell script
docker-compose exec node serverless deploy --stage prod --region us-east-1
```

### Without Docker

```shell script
serverless deploy --stage prod --region us-east-1
```

This will deploy the project to `us-east-1`

**Deployment Output**

```shell script
Serverless: Packaging service...
Serverless: Excluding development dependencies...
Serverless: Uploading CloudFormation file to S3...
Serverless: Uploading artifacts...
Serverless: Uploading service monitor.zip file to S3 (1.37 MB)...
Serverless: Validating template...
Serverless: Updating Stack...
Serverless: Checking Stack update progress...
...........
Serverless: Stack update finished...
Service Information
service: monitor
stage: prod
region: us-east-1
stack: monitor-prod
resources: 9
api keys:
  None
endpoints:
  None
functions:
  http: monitor-prod-http
layers:
  None
Serverless: Run the "serverless" command to setup monitoring, troubleshooting and testing.
```

A quick look at the Resources created by AWS using CloudFormation

<img src="https://raw.githubusercontent.com/akki-io/serverless-monitor/master/images/resources.jpg" alt="serverless-monitor-resources">


## Local Tinkering

### With Docker

**Invoke the cloud function**
 
```shell script
docker-compose exec node \
	serverless invoke \
	--stage prod --region us-east-1 --function http \
	--data '["https://www.google.com"]'
```

**Invoke the local copy of the function**

```shell script
docker-compose exec node \
	serverless invoke local \
	--stage prod --function http \
	--data '["https://www.google.com"]'
```

### Without Docker

**Invoke the cloud function**
 
```shell script
serverless invoke \
    --stage prod --region us-east-1 --function http \
	--data '["https://www.google.com"]'
```

**Invoke the local copy of the function**

```shell script
serverless invoke local \
	--stage prod --function http \
	--data '["https://www.google.com"]'
```

You will then see an output similar to below.

```shell script
endpoints: [ 'https://www.google.com' ]
Requesting https://www.google.com
https://www.google.com : {"statusCode":200,"durationMS":229.07045600000015}
Final results:
{"https://www.google.com":{"statusCode":200,"durationMS":229.07045600000015}}
{
    "https://www.google.com": {
        "statusCode": 200,
        "durationMS": 229.07045600000015
    }
}
Logged metrics in Cloudwatch at: serverless-monitor
```

## Screenshots

**Slack Alerts**

<img src="https://raw.githubusercontent.com/akki-io/serverless-monitor/master/images/slack-alert.jpg" alt="serverless-monitor-resources">

**CloudWatch Graph**

<img src="https://raw.githubusercontent.com/akki-io/serverless-monitor/master/images/chart.jpg" alt="serverless-monitor-resources">


## Contributions
All contributions are welcomed, please create a Pull Request.

## Credits
- [lambda-ping](https://github.com/jethrocarr/lambda-ping) - Inspiration

## Todo

- AWS SNS subscription
- Maybe Cost Estimation
- ... suggestions?

## Donations
- [Plant a tree](https://offset.earth/) 

## License
Licensed under the MIT license.

Built with <span style="color: #e25555;padding: 0px 3px;">♥</span> in <img src="https://raw.githubusercontent.com/akki-io/serverless-monitor/master/images/ca.png" alt="Canada" width="20"> </div>
