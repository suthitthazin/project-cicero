# Project Cicero

## Local Setup

1. Ensure NodeJS is installed and the AWS CDK toolkit is set up [correctly](https://docs.aws.amazon.com/cdk/latest/guide/work-with.html#work-with-prerequisites). To get your AWS credentials with your educate account click the account details button before signing in and copy and paste the CLI details into the .aws folder. 
2. If you run into errors this project was successfully deployed with version 1.94.1 of the Node aws_cdk library. To explicitly install it run:
   
   `> npm install -g aws-cdk@1.94.1`
4. Install the CDK toolkit version
   ![](https://user-images.githubusercontent.com/31460379/112003536-5d314f80-8af7-11eb-8912-1a53db51ce73.png)
    `> vim ~/.aws/credentials`
2. Make sure Python 3.6 or higher is [installed](https://www.python.org/downloads/) along with pip and virtualenv packages.
3. Source virtual environment for Python packages.

    `> source .venv/bin/activate`
4. Install packages.

    `> pip install -r requirements.txt`

5. [Verify an email to use for SNS service](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-email-addresses-procedure.html)
   You can also verify email using boto3
   ```
   def verify_email_identity():
    ses_client = boto3.client("ses", region_name="us-east-2")
    response = ses_client.verify_email_identity(
        EmailAddress="abc1234@rit.edu"
    )
    print(response)
    ```
    This MUST be done for the sender email. The recipient email must also be verified if you are using SES in sandbox mode.
    Note: SES does not work on AWS Educate. Use a regular or free tier.

6. Make sure that Docker is running locally

7. Profit

For more information on how to add modules and documentation on modules check out the AWS [docs](https://docs.aws.amazon.com/cdk/latest/guide/work-with-cdk-python.html). Make sure any new modules are added to `requirements.txt` with correct versioning.


## Supported Language Codes

| Language                  | Input Language Code | Target Language Code |
| ------------------------- | ------------------- | -------------------- |
| Arabic (Gulf / Modern)    | ar-AE / ar-SA       | arb                  |
| Chinese (Mandarin)        | zh-CN               | cmn-CN               |
| Danish                    | Input not supported | da-DK                |
| Dutch                     | nl-NL               | nl-NL                |
| English (Australian)      | en-AU               | en-AU                |
| English (British)         | en-GB               | en-GB                |
| English (Indian)          | en-IN               | Output not supported |
| English (US)              | en-US               | en-US                |
| Farsi Persian             | fa-IR               | Output not supported |
| French                    | fr-FR               | fr-FR                |
| French (Canadian)         | fr-CA               | fr-CA                |
| German (Standard / Swiss) | de-DE / de-CH       | de-DE                |
| Hebrew                    | he-IL               | Output not supported |
| Hindi                     | hi-IN               | hi-IN                |
| Icelandic                 | Input not supported | is-IS                |
| Indonesian                | id-ID               | Output not supported |
| Italian                   | it-IT               | it-IT                |
| Japanese                  | ja - JP             | ja-JP                |
| Korean                    | ko-KR               | ko-KR                |
| Malaysian                 | ms-MY               | Output not supported |
| Norwegian                 | Input not supported | nb-NO                |
| Polish                    | Input not supported | pl-PL                |
| Portugese (Brazilian)     | pt-BR               | pt-BR                |
| Portugese (European)      | pt-PT               | pt-PT                |
| Romanian                  | Input not supported | ro-RO                |
| Russian                   | ru-RU               | ru-RU                |
| Spanish (European)        | es-ES               | es-ES                |
| Spanish (Mexican)         | Input not supported | es-MX                |
| Spanish (US)              | es-US               | es-US                |
| Swedish                   | Input not supported | sv-SE                |
| Tamil                     | ta-IN               | Output not supported |
| Telugu                    | te-IN               | Output not supported |
| Turkish                   | tr-TR               | tr-TR                |
| Welsh                     | Input not supported | cy-GB                |

## Synthesize and Deploy
Stacks can be simply synthesized into Cloudformation templates or directly deployed from the command line.

### Bootstrap (do this first)
`> cdk bootstrap`

### Synthesize
`> cdk synth`

### Deploy
`> cdk deploy`

### Destroy
`> cdk destroy`

## Actually using it

1. Deploy the stack using the steps above.

2. Find the location of the static site's S3 URL. When the bucket is made it is automatically public and available for static usage.

3. Once on the website fill in the required information. This includes the API URL from the gateway. This was necessary due to the order in which the resources are created. The URL was not known at the time of creating the static site. The language codes can be found in a section above. As a disclaimer we have run into some transient issues with large video files. So if that is an issue try with a smaller video.

4. Once submitted the video should begin processing. You may look at the individual buckets to see the flow of data. Once the video is finished it is placed in the finished video bucket. If your email address was verified you should also receive an email with a link to your finished video.
