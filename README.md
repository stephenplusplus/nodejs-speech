<img src="https://avatars2.githubusercontent.com/u/2810941?v=3&s=96" alt="Google Cloud Platform logo" title="Google Cloud Platform" align="right" height="96" width="96"/>

# Google Cloud Speech API: Node.js Client

[![release level](https://img.shields.io/badge/release%20level-beta-yellow.svg?style&#x3D;flat)](https://cloud.google.com/terms/launch-stages)
[![CircleCI](https://img.shields.io/circleci/project/github/googleapis/nodejs-speech.svg?style=flat)](https://circleci.com/gh/googleapis/nodejs-speech)
[![AppVeyor](https://ci.appveyor.com/api/projects/status/github/googleapis/nodejs-speech?svg=true)](https://ci.appveyor.com/project/googleapis/nodejs-speech)
[![codecov](https://img.shields.io/codecov/c/github/googleapis/nodejs-speech/master.svg?style=flat)](https://codecov.io/gh/googleapis/nodejs-speech)

> Node.js idiomatic client for [Speech API][product-docs].

The [Cloud Speech API](https://cloud.google.com/speech/docs) enables easy integration of Google speech recognition technologies into developer applications. Send audio and receive a text transcription from the Cloud Speech API service.

* [Speech API Node.js Client API Reference][client-docs]
* [Speech API Documentation][product-docs]

Read more about the client libraries for Cloud APIs, including the older
Google APIs Client Libraries, in [Client Libraries Explained][explained].

[explained]: https://cloud.google.com/apis/docs/client-libraries-explained

**Table of contents:**

* [Quickstart](#quickstart)
  * [Before you begin](#before-you-begin)
  * [Installing the client library](#installing-the-client-library)
  * [Using the client library](#using-the-client-library)
* [Samples](#samples)
* [Versioning](#versioning)
* [Contributing](#contributing)
* [License](#license)

## Quickstart

### Before you begin

1.  Select or create a Cloud Platform project.

    [Go to the projects page][projects]

1.  Enable billing for your project.

    [Enable billing][billing]

1.  Enable the Google Cloud Speech API API.

    [Enable the API][enable_api]

1.  [Set up authentication with a service account][auth] so you can access the
    API from your local workstation.

[projects]: https://console.cloud.google.com/project
[billing]: https://support.google.com/cloud/answer/6293499#enable-billing
[enable_api]: https://console.cloud.google.com/flows/enableapi?apiid=speech.googleapis.com
[auth]: https://cloud.google.com/docs/authentication/getting-started

### Installing the client library

    npm install --save @google-cloud/speech

### Using the client library

```javascript
// Imports the Google Cloud client library
const Speech = require('@google-cloud/speech');
const fs = require('fs');

// Your Google Cloud Platform project ID
const projectId = 'your-project-id';

// Instantiates a client
const speechClient = Speech({
  projectId: projectId
});

// The name of the audio file to transcribe
const fileName = './resources/audio.raw';

// Reads a local audio file and converts it to base64
const file = fs.readFileSync(fileName);
const audioBytes = file.toString('base64');

// The audio file's encoding, sample rate in hertz, and BCP-47 language code
const audio = {
  content: audioBytes
};
const config = {
  encoding: 'LINEAR16',
  sampleRateHertz: 16000,
  languageCode: 'en-US'
};
const request = {
  audio: audio,
  config: config
};

// Detects speech in the audio file
speechClient.recognize(request)
  .then((data) => {
    const response = data[0];
    const transcription = response.results.map(result =>
        result.alternatives[0].transcript).join('\n');
    console.log(`Transcription: ${transcription}`);
  })
  .catch((err) => {
    console.error('ERROR:', err);
  });
```

## Samples

Samples are in the [`samples/`](https://github.com/blob/master/samples) directory. The samples' `README.md`
has instructions for running the samples.

| Sample                      | Source Code                       |
| --------------------------- | --------------------------------- |
| Recognize | [source code](https://github.com/googleapis/nodejs-speech/blob/master/samples/recognize.js) |

The [Speech API Node.js Client API Reference][client-docs] documentation
also contains samples.

## Versioning

This library follows [Semantic Versioning](http://semver.org/).

This library is considered to be in **beta**. This means it is expected to be
mostly stable while we work toward a general availability release; however,
complete stability is not guaranteed. We will address issues and requests
against beta libraries with a high priority.

More Information: [Google Cloud Platform Launch Stages][launch_stages]

[launch_stages]: https://cloud.google.com/terms/launch-stages

## Contributing

Contributions welcome! See the [Contributing Guide](.github/CONTRIBUTING.md).

## License

Apache Version 2.0

See [LICENSE](LICENSE)

[client-docs]: https://cloud.google.com/nodejs/docs/reference/speech/latest/
[product-docs]: https://cloud.google.com/speech/docs
