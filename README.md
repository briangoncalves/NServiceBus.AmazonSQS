NServiceBus.AmazonSQS
===============

This is an Amazon SQS transport for NServiceBus V5. It currently in the early stages of development but should be stable enough for serious users. If you'd like to get up and running quickly, follow the below steps!

Feel free to browse and contribute!

### Set Up An AWS Account
You will need an [AWS IAM](http://docs.aws.amazon.com/IAM/latest/UserGuide/IAM_Introduction.html) account with a pair of [Access Keys](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSGettingStartedGuide/AWSCredentials.html) to use NServiceBus.AmazonSQS. 
The account needs the following permissions:
* SQS::CreateQueue
* SQS::DeleteMessage
* SQS::GetQueueUrl
* SQS::ReceiveMessage
* SQS::SendMessage
* S3::PutBucket
* S3::DeleteObject
* S3::GetObject
* S3::PutObject
* S3::PutLifecycleConfiguration

Once you have a pair of Access Keys (Access Key ID and Secret Access Key), you will need to store them in environment variables of the machine that is running your endpoint:
* Access Key ID goes in AWS_ACCESS_KEY_ID 
* Secret Access Key goes in AWS_SECRET_ACCESS_KEY

### Install The NuGet Package

    PM> Install-Package NServiceBus.AmazonSQS

See the [NuGet Gallery](https://www.nuget.org/packages/NServiceBus.AmazonSQS) for details. 

### Configure Your Endpoint
When self-hosting:

    busConfiguration
        .UseTransport<NServiceBus.SqsTransport>()

When hosting in the NServiceBus.Host: 

    public class EndpointConfig : 
        IConfigureThisEndpoint, 
        AsA_Server, // Or AsA_Client, whatever
        UsingTransport<NServiceBus.SqsTransport>

Add a connection string to your app.config (or web.config):

    <connectionStrings>
        <add name="NServiceBus/Transport" connectionString="Region=ap-southeast-2;S3BucketForLargeMessages=myBucketName;S3KeyPrefix=my/key/prefix;" />
    </connectionStrings>

And you should be good to go!

For more documentation on what you can pass to the connection string, check out [this page](https://github.com/ahofman/NServiceBus.AmazonSQS/wiki/Configuration-Options).
