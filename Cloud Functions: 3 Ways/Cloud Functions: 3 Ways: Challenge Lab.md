## `Lab Name` - Cloud Functions: 3 Ways: Challenge Lab [ARC104]
## `Lab Link` - [*Click Here*](https://www.cloudskillsboost.google/focuses/61974?parent=catalog)

Click `Activate Cloud Shell`
```bash
gcloud auth list
```
Click `Authorize`.
```bash
gcloud config list project
```
### Enable APIs

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

```bash
export REGION=us-west1
export HTTP_FUNCTION=http-messenger
export FUNCTION_NAME=cs-tracker
export BUCKET="gs://$DEVSHELL_PROJECT_ID"
```

### Task 1. Create a Cloud Storage bucket

`Setup`
To use Cloud Storage functions, first grant the pubsub.publisher IAM role to the Cloud Storage service account:
```bash
PROJECT_NUMBER=$(gcloud projects list --filter="project_id:$PROJECT_ID" --format='value(project_number)')
SERVICE_ACCOUNT=$(gsutil kms serviceaccount -p $PROJECT_NUMBER)
gcloud projects add-iam-policy-binding $PROJECT_ID \
  --member serviceAccount:$SERVICE_ACCOUNT \
  --role roles/pubsub.publisher
```

```bash
gsutil mb -l $REGION gs://$DEVSHELL_PROJECT_ID
```

Check my progress 

### Task 2. Create, deploy, and test a Cloud Storage function (2nd gen)

`Create`
Run the following command to create the folder and files for the app and navigate to the folder:
```bash
mkdir ~/hello-storage && cd $_
touch index.js && touch package.json
```

Add the following code to the `hello-storage/index.js` file that simply responds to Cloud Storage events:
```bash
const functions = require('@google-cloud/functions-framework');

functions.cloudEvent('eventStorage', (cloudevent) => {
  console.log('A new event in your Cloud Storage bucket has been logged!');
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
gcloud functions deploy cs-tracker \
  --gen2 \
  --runtime nodejs20 \
  --entry-point cs-tracker \
  --source . \
  --region $REGION \
  --trigger-bucket $BUCKET \
  --trigger-location $REGION \
  --max-instances 2
```

Check my progress 

### Task 3. Create and deploy a HTTP function (2nd gen) with minimum instances

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
  res.status(200).send('HTTP function (2nd gen) has been called!');
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
gcloud functions deploy  http-messenger \
  --gen2 \
  --runtime nodejs20 \
  --entry-point http-messenger \
  --source . \
  --region $REGION \
  --trigger-http \
  --timeout 600s \
  --max-instances 2 \
  --min-instances 1
```

## Congratulation!