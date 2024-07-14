## Speech-to-Text API: Qwik Start

### Task 1. Create an API key

1. To create an API key, click Navigation menu > APIs & services > Credentials. 
2. Then click Create credentials. 
3. In the drop down menu, select API key. 
4. Copy the key you just generated and click Close.

Click Check my progress 

1. In the Navigation menu, select Compute Engine. You should see a linux-instance listed in the VM instances window. 
2. Click on the SSH button in line with the linux-instance. You will be brought to an interactive shell. 
3. In the command line, enter in the following, replacing <YOUR_API_KEY> with the API key you copied from previously generated: 
export API_KEY=AIzaSyDYcwwTSNuYs0sjw-oAYJcdu9nQ9kB8aXo

### Task 2. Create your Speech-to-Text API request

1. Create request.json in the SSH command line. You'll use this to build your request to the Speech-to-Text API:
touch request.json

2. Open the request.json:
nano request.json

3. Add the following to your request.json file, using the uri value of the sample raw audio file:

{
  "config": {
      "encoding":"FLAC",
      "languageCode": "en-US"
  },
  "audio": {
      "uri":"gs://cloud-samples-tests/speech/brooklyn.flac"
  }
}

4. Press control + x and then y to save and click Enter to close the request.json file.

Click Check my progress

### Task 3. Call the Speech-to-Text API

1. Pass your request body, along with the API key environment variable, to the Speech-to-Text API with the following curl command (all in one single command line):
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json \
"https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}"
2. Run the following command to save the response in a result.json file:
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json \
"https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}" > result.json

Click Check my progress 

## Congratulations!

