# Serverless WebSockets chat based on AWS IoT

This is the source code for the [Serverless AWS IoT tutorial](https://BLOG-POST-LINK-HERE). Read below for how to set it up.

## Set up the project

- Log in into your AWS account or set up one https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/

- Create `serverless-deployer` IAM user
  - Navigate IAM -> Users and click "Add User"
  - Set "User name" to `serverless-deployer`
  - Set "Access type" to "Programmatic access" and click "Next"
  - Click "Attach existing policies directly"
  - Select "AdministratorAccess" from the list and click "Next"
  - Review information and click "Create user"
  - Click "Download .csv"

- Create `iot-connector` IAM user
  - Navigate IAM -> Users and click "Add User"
  - Set "User name" to `iot-connector`
  - Set "Access type" to "Programmatic access" and click "Next"
  - Click "Attach existing policies directly"
  - Select "AWSIoTDataAccess" from the list and click "Next"
  - Review information and click "Create user"
  - Click "Download .csv"

- Create a folder for the project: `mkdir serverless-aws-iot; cd serverless-aws-iot`

- Clone the repository: `git clone https://github.com/gettechtalent/REPO-LINK-HERE.git`

## Set up the backend

- Navigate to the backend folder: `cd backend`

- Install serverless: `npm install -g serverless`

- Configure serverless from the `serverless-deployer` .csv file
`serverless config credentials --provider aws --key <Access key ID> --secret <Secret access key> --profile serverless-demo`

- Edit `serverless.yml`. Under the `provider` section set the `region` to where your AWS Lambda functions will live. Also, make sure to set the `IOT_AWS_REGION` environment variable in the same file.

- Set `IOT_ACCESS_KEY` and `IOT_SECRET_KEY` from the `iot-connector` .csv file

- In the AWS console navigate to AWS IoT -> Settings. Set the `IOT_ENDPOINT_HOST` variable in the `serverless.yml` to the `Endpoint` that you see on the page.

- Install serverless: `npm install -g serverless`

- Install the dependencies: `npm install`

- Start up the lambdas locally: `serverless offline --port 8080 start`. You should see something like this:
```bash
Serverless: Starting Offline: dev/eu-west-1.

Serverless: Routes for iotPresignedUrl:
Serverless: OPTIONS /iot-presigned-url
Serverless: GET /iot-presigned-url

Serverless: Routes for notifyDisconnect:

Serverless: Offline listening on http://localhost:8080
```

- Navigate in the browser to `localhost:8080/iot-presigned-url`. You should see something like this:
`{"url":"wss://3kdfgh39sdfyrte.iot.eu-west-1.amazonaws.com/mqtt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=DSJHGRJWFICUIYWEFSSD%2F20170529%2Feu-west-1%2Fiotdevicegateway%2Faws4_request&X-Amz-Date=20170529T063531Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=435876t863fd8fk43jtygdf34598e9ghdrt439g8rytk34hfd9854y3489tfydee"}`

## Set up the frontend

- Navigate to the frontend folder: `cd ../frontend`

- Install the dependencies: `npm install`

- Start up the front-end locally: `npm start`. You should see something like this:
```bash
Compiled successfully!

You can now view frontend in the browser.

  Local:            http://localhost:3000/
  On Your Network:  http://192.168.0.1:3000/

Note that the development build is not optimized.
To create a production build, use npm run build.
```

- Navigate in the browser to `localhost:3000`. You should see the Serverless IoT WebSockets chat app in action.

- Feel free to open several browser tabs with the app and send some chat messages. You will see `Connected users` as well as `Messages` sections populated.