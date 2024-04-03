# Shotstack MP4 to WEBM Demo

This sample application shows how you can use the Shotstack Ingest API to [convert MP4 videos to WEBM](https://shotstack.io/demo/mp4-to-webm/) format. The Ingest API is a [video transformation API](https://shotstack.io/product/ingest-api/) that lets you upload, store, and convert videos and images into different formats, sizes, frame rates, speeds, and more.

Using an HTML web form, users can upload a video or put in a URL of an MP4 video online. After submitting the form, the video is converted from MP4 to WEBM. Users can play the new webm file in their browsers or download it.

View the live demo at: https://shotstack.io/demo/mp4-to-webm/

The demo is made with Node.js and works with the Express Framework or as a serverless project using AWS Lambda and API Gateway.

### Requirements

- Node 16+
- Shotstack API key: https://dashboard.shotstack.io/register

### Project Structure

The project is divided into two components:

#### Backend API

The backend API has an endpoint that receives the video file URL. The parameters are prepared in the [JSON format](https://shotstack.io/docs/api/#tocs_source) the Ingest API expects and sent to the API. A status endpoint is called to check the progress of the transformation. When the webm file is ready, the status is updated and the file URL of the webm file is returned.

The backend API source code is in the **api** directory.

#### Frontend Web Form & Player

The frontend uses Bootstrap and basic HTML to set up a form that allows the user to upload a video file or enter a file URL. We use jQuery for the interactive components of the application, to submit the data to the backend API and poll the status. There is also a video player that plays the final webm video file when it's ready.

The source code for the frontend is in the **web** directory.

### Installation

Install node module dependencies:

```bash
cd api
npm install
```

### Configuration

Copy the `.env.dist` file and rename it `.env`:

```
cp .env.dist .env
```

Replace the environment variables below with your Shotstack API key (stage key) and a writable S3 bucket name:

```bash
SHOTSTACK_API_KEY=replace_with_your_shotstack_key
SHOTSTACK_HOST=https://api.shotstack.io/ingest/stage/
AWS_S3_UPLOADS_BUCKET=replace_with_an_s3_bucket_name
```

### Run Locally

To start the API and serve the frontend form (from the **api** directory):

Navigat to the **api** directory. And run the command below to start the API and serve the frontend form.

```bash
npm run start
```

Then visit [http://localhost:3000](http://localhost:3000).


### Deploy Serverless Application (optional)

The project has been built as a serverless application using the Serverless Framework and AWS Lambda. To understand more about the Serverless Framework and how to set everything up consult the documentation:
https://serverless.com/framework/docs/providers/aws/

To deploy to AWS Lambda (from the **api** directory):

```bash
npm run deploy
```

Once the API is deployed set the `var apiEndpoint` variable in **web/app.js** to the returned API Gateway URL.

Run the **web/index.html** file locally or use AWS S3 static hosting to serve the web page.
