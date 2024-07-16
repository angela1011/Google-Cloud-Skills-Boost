## Cloud Functions 2nd Gen: Qwik Start

Click `Activate Cloud Shell`
```bash
gcloud auth list
```
Click `Authorize`.
```bash
gcloud config list project
```

### Task 1. Enable APIs

In Cloud Shell, run the following command to set your Project ID variable.
```bash
export PROJECT_ID=$(gcloud config get-value project)
```

Run the following command to set the Region variable.
```bash
export REGION=us-west1
gcloud config set compute/region $REGION
```

Execute the following command to enable all necessary services.
```bash
gcloud services enable \
  artifactregistry.googleapis.com \
  cloudfunctions.googleapis.com \
  cloudbuild.googleapis.com \
  eventarc.googleapis.com \
  run.googleapis.com \
  logging.googleapis.com \
  pubsub.googleapis.com
```

Check my progress 

### Task 2. Create an HTTP function

`Create`
Run the following command to create the folder and files for the app and navigate to the folder:
```bash
mkdir ~/hello-http && cd $_
touch index.js && touch package.json
```
Click the Open `Editor` button on the toolbar of Cloud Shell. (You can switch between Cloud Shell and the code editor by using the Open Editor and Open Terminal icons as required, or click the Open in new window button to leave the Editor open in a separate tab).

In the Editor, add the following code to the `hello-http/index.js` file that simply responds to HTTP requests:

```bash
const functions = require('@google-cloud/functions-framework');

functions.http('helloWorld', (req, res) => {
  res.status(200).send('HTTP with Node.js in GCF 2nd gen!');
});
```
Add the following content to the `hello-http/package.json` file to specify the dependencies.

```bash
{
  "name": "nodejs-functions-gen2-codelab",
  "version": "0.0.1",
  "main": "index.js",
  "dependencies": {
    "@google-cloud/functions-framework": "^2.0.0"
  }
}
```
Check my progress 

`Deploy`
In Cloud Shell, run the following command to deploy the function:
```bash
gcloud functions deploy nodejs-http-function \
  --gen2 \
  --runtime nodejs18 \
  --entry-point helloWorld \
  --source . \
  --region $REGION \
  --trigger-http \
  --timeout 600s \
  --max-instances 1
```

`Test`
Test the function with the following command:
```bash
gcloud functions call nodejs-http-function \
  --gen2 --region $REGION
```

### Task 3. Create a Cloud Storage function

`Setup`
To use Cloud Storage functions, first grant the pubsub.publisher IAM role to the Cloud Storage service account:

```bash
PROJECT_NUMBER=$(gcloud projects list --filter="project_id:$PROJECT_ID" --format='value(project_number)')
SERVICE_ACCOUNT=$(gsutil kms serviceaccount -p $PROJECT_NUMBER)
```

```bash
gcloud projects add-iam-policy-binding $PROJECT_ID \
  --member serviceAccount:$SERVICE_ACCOUNT \
  --role roles/pubsub.publisher
```

`Create`
Run the following command to create the folder and files for the app and navigate to the folder:
```bash
mkdir ~/hello-storage && cd $_
touch index.js && touch package.json
```

Add the following code to the `hello-storage/index.js` file that simply responds to Cloud Storage events:
```bash
const functions = require('@google-cloud/functions-framework');

functions.cloudEvent('helloStorage', (cloudevent) => {
  console.log('Cloud Storage event with Node.js in GCF 2nd gen!');
  console.log(cloudevent);
});
```

Add the following content to the `hello-storage/package.json` file to specify the dependencies:
```bash
{
  "name": "nodejs-functions-gen2-codelab",
  "version": "0.0.1",
  "main": "index.js",
  "dependencies": {
    "@google-cloud/functions-framework": "^2.0.0"
  }
}
```

`Deploy`
First, create a Cloud Storage bucket to use for creating events:
```bash
BUCKET="gs://gcf-gen2-storage-$PROJECT_ID"
gsutil mb -l $REGION $BUCKET
```

Deploy the function:
```bash
gcloud functions deploy nodejs-storage-function \
  --gen2 \
  --runtime nodejs18 \
  --entry-point helloStorage \
  --source . \
  --region $REGION \
  --trigger-bucket $BUCKET \
  --trigger-location $REGION \
  --max-instances 1
```

`Test`
Test the function by uploading a file to the bucket:
```bash
echo "Hello World" > random.txt
gsutil cp random.txt $BUCKET/random.txt
```

Run the following command. You should see the received CloudEvent in the logs:
```bash
gcloud functions logs read nodejs-storage-function \
  --region $REGION --gen2 --limit=100 --format "value(log)"
```

Check my progress 

### Task 4. Create a Cloud Audit Logs function

From the `Navigation Menu`, go to `IAM & Admin` -> `Audit Logs`.

Find the `Compute Engine API` and click the `check box` next to it. If you are unable to find the API, search it on next page.

On the info pane on the right, check `Admin Read`, `Data Read`, and `Data Write log types` and click `Save`.

Grant the default Compute Engine service account the eventarc.eventReceiver IAM role:
```bash
gcloud projects add-iam-policy-binding $PROJECT_ID \
  --member serviceAccount:$PROJECT_NUMBER-compute@developer.gserviceaccount.com \
  --role roles/eventarc.eventReceiver
```

`Get the code`
Run the following code to clone the repo that contains the application:
```bash
cd ~
git clone https://github.com/GoogleCloudPlatform/eventarc-samples.git
```

Navigate to the app directory:
```bash
cd ~/eventarc-samples/gce-vm-labeler/gcf/nodejs
```

`Deploy`
Deploy the function with gcloud as before. Notice how the function is filtering on Audit Logs for Compute Engine insertions with the --trigger-event-filters flag:
```bash
gcloud functions deploy gce-vm-labeler \
  --gen2 \
  --runtime nodejs18 \
  --entry-point labelVmCreation \
  --source . \
  --region $REGION \
  --trigger-event-filters="type=google.cloud.audit.log.v1.written,serviceName=compute.googleapis.com,methodName=beta.compute.instances.insert" \
  --trigger-location $REGION \
  --max-instances 1
```

Check my progress

`Test`
From the `Navigation Menu`, go to `Compute Engine` -> `VM instances`.

Click `Create Instance`.

Leave all of the fields as the default values and click `Create`.

Verify using the following command:

```bash
gcloud compute instances describe instance-1 --zone ""
```

Check my progress

Run the following command to delete the VM. Type `Y` when prompted to confirm.
```bash
gcloud compute instances delete instance-1 --zone ""
```
### Task 5. Deploy different revisions

`Create`
Run the following command to create the folder and files for the app and navigate to the folder:
```bash
mkdir ~/hello-world-colored && cd $_
touch main.py
touch requirements.txt
```

Add the following code to the hello-world-colored/main.py file with a Python function that reads a color environment variable and responds back with Hello World in that background color:
```bash
import os

color = os.environ.get('COLOR')

def hello_world(request):
    return f'<body style="background-color:{color}"><h1>Hello World!</h1></body>'
```

Deploy
Deploy the first revision of the function with an orange background:
```bash
COLOR=orange
gcloud functions deploy hello-world-colored \
  --gen2 \
  --runtime python39 \
  --entry-point hello_world \
  --source . \
  --region $REGION \
  --trigger-http \
  --allow-unauthenticated \
  --update-env-vars COLOR=$COLOR \
  --max-instances 1
```
Navigate to the Cloud Functions page in the Console and click the hello-world-colored function.

On the top right of the page under Powered by Cloud Run click hello-world-colored.

This will re-direct you to the Cloud Run service page.

Click the Revisions tab and then select Edit & Deploy New Revision.

Leave everything as default and scroll down and select Variables & Secrets tab and in Environment Variables section. Update the COLOR environment variable to yellow.

Click Deploy.

Check my progress

### Task 6. Set up minimum instances

Create
Run the following command to create the folder and files for the app and navigate to the folder:
```bash
mkdir ~/min-instances && cd $_
touch main.go
touch go.mod
```

Add the following code to the min-instances/main.go file. This Go service has an init function that sleeps for 10 seconds to simulate a long initialization. It also has a HelloWorld function that responds to HTTP calls:
```bash
package p

import (
        "fmt"
        "net/http"
        "time"
)

func init() {
        time.Sleep(10 * time.Second)
}

func HelloWorld(w http.ResponseWriter, r *http.Request) {
        fmt.Fprint(w, "Slow HTTP Go in GCF 2nd gen!")
}
```

Add the following code to the min-instances/go.mod file. This specifies the module path and Go language version:
```bash
module example.com/mod

go 1.16
```

Deploy
Run the following command to deploy the first revision of the function with the default minimum instance value of zero:
```bash
gcloud functions deploy slow-function \
  --gen2 \
  --runtime go116 \
  --entry-point HelloWorld \
  --source . \
  --region $REGION \
  --trigger-http \
  --allow-unauthenticated \
  --max-instances 4
```

Test the function with this command:
```bash
gcloud functions call slow-function \
  --gen2 --region $REGION
```
Set minimum instances

Navigate to the Cloud Run page in the Console and click the slow-function service.

Click the Revisions tab and then select Edit & Deploy New Revision.

Under the Autoscaling section, set Minimum number of instances to 1 and Maximum number of instances to 4.

Leave the rest of the fields as default and click Deploy.

Test
Test the function again:
```bash
gcloud functions call slow-function \
  --gen2 --region $REGION
```

Check my progress 

### Task 7. Create a function with concurrency

Test without concurrency
Run the following command to get the URL of the function and save it as an environment variable:
```bash
SLOW_URL=$(gcloud functions describe slow-function --region $REGION --gen2 --format="value(serviceConfig.uri)")
```

Use an open source benchmarking tool called hey to send 10 concurrent requests to the slow function. hey is already installed in Cloud Shell:
```bash
hey -n 10 -c 10 $SLOW_URL
```

Run the following command to delete the function. Type Y when prompted to confirm.
```bash
gcloud run services delete slow-function --region ""
```

Deploy
Deploy a new function identical to the previous function. Once deployed, you will increase its concurrency:
```bash
gcloud functions deploy slow-concurrent-function \
  --gen2 \
  --runtime go116 \
  --entry-point HelloWorld \
  --source . \
  --region $REGION \
  --trigger-http \
  --allow-unauthenticated \
  --min-instances 1 \
  --max-instances 4
```

Set concurrency

From the Navigation Menu, go to Cloud Run.

Click the slow-concurrent-function service.

Click the Revisions tab and then select Edit & Deploy New Revision.

Under the Resources section, set the CPU to 1.

Under Requests, set the Maximum concurrent requests per instance to 100.

Under Autoscaling, set the Maximum number of instances to 4.

Leave the rest of the fields as default and click Deploy.

Test with concurrency
Once your function has deployed, run the following command to get the URL of the new function and save it as an environment variable:
```bash
SLOW_CONCURRENT_URL=$(gcloud functions describe slow-concurrent-function --region $REGION --gen2 --format="value(serviceConfig.uri)")
```
Now use hey to send 10 concurrent requests:
```bash
hey -n 10 -c 10 $SLOW_CONCURRENT_URL
```

Check my progress

## Congratulation!