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

```bash

```

```bash

```

```bash

```

```bash

```
## Congratulation!