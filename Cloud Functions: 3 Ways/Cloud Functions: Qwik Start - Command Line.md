## Cloud Functions: Qwik Start - Command Line

```bash
gcloud auth list
```
Click Authorize.
```bash
gcloud config list project
```

### Task 1. Create a function: 
```bash
gcloud config set compute/region REGION
```
Create a directory :
```bash
mkdir gcf_hello_world
```
Entry:
```bash
cd gcf_hello_world
```
Edit:
```bash
nano index.js
```
Copy paste:
```bash
/**
* Background Cloud Function to be triggered by Pub/Sub.
* This function is exported by index.js, and executed when
* the trigger topic receives a message.
*
* @param {object} data The event payload.
* @param {object} context The event metadata.
*/
exports.helloWorld = (data, context) => {
const pubSubMessage = data;
const name = pubSubMessage.data
    ? Buffer.from(pubSubMessage.data, 'base64').toString() : "Hello World";

console.log(`My Cloud Function: ${name}`);
};
```
Exit nano (Ctrl+x) and save (Y) the file.

### Task 2. Create a Cloud Storage bucket
```bash
gsutil mb -p [PROJECT_ID] gs://[BUCKET_NAME]
```
Check my progress

### Task 3. Deploy your function
Disable the Cloud Functions API:
```bash
gcloud services disable cloudfunctions.googleapis.com
```
Re-enable the Cloud Functions API:
```bash
gcloud services enable cloudfunctions.googleapis.com
```
```bash
gcloud projects add-iam-policy-binding [PROJECT_ID] \
--member="serviceAccount:[PROJECT_ID]@appspot.gserviceaccount.com" \
--role="roles/artifactregistry.reader"
```

```bash
gcloud functions deploy helloWorld \
  --stage-bucket [BUCKET_NAME] \
  --trigger-topic hello_world \
  --runtime nodejs20
```
enter Y

```bash
gcloud functions describe helloWorld
```
Check my progress
### Task 4. Test the function
```bash
DATA=$(printf 'Hello World!'|base64) && gcloud functions call helloWorld --data '{"data":"'$DATA'"}'
```
### Task 5. View logs
```bash
gcloud functions logs read helloWorld
```

### Task 6. Test your understanding
### Serverless lets you write and deploy code without the hassle of managing the underlying infrastructure.
```bash
True
```

## Congratulation!