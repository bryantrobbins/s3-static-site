# S3 Static Site

An AWS CloudFormation template to build an S3 static website behind a Cloudfront
distribution.

## Requirements

You need an existing Route53 Hosted Zone to reference.

You need to receive e-mail to one of the following e-mail addresses in
that domain:
* hostmaster@...
* admin@...
* postmaster@...
* administrator@...
* webmaster@...

## Parameters

* **SiteHostName**: The "hostname" portion of the URL for the S3 Static Site you are
creating.  For example, if you were creating the site www.example.com, the
hostname portion is www.
* **SiteDomainName**: The "domain name" portion of the URL for the S3 Static Site you
are creating.  For example, if you were creating the site\nwww.example.com,
the domain name portion is example.com.  The domain\nname should NOT end in
a period.
* **DefaultTTL**: The default TTL, in seconds, for items in the CloudFront cache
that do not have cache header information.  The default is set
low, under the assumption you will be developing your site.
Once in production, you should increase this value apropriately
(such as the AWS default of 86400).
* **PriceClass**: Describes the global scope for your CloudFront distribution.
Allowed values are 100, 200, and ALL.
  * 100: Use Only US, Canada and Europe
  * 200: Use Only US, Canada, Europe, and Asia
  * ALL: Use All Edge Locations (Best Performance)

## Launching Stack

The stack build will take 30+ minutes, due to the length of time
Cloudfront takes to provision.  In addition, it will require manual
verification for the SSL certificate the stack creates.

```
% aws cloudformation create-stack --stack-name example-stack \
  --template-body file://s3-static-site.yaml \
  --parameters
      ParameterKey=SiteHostName,ParameterValue=test
      ParameterKey=SiteDomainName,ParameterValue=ratemytank.com
```

### Adding Content

Copy static assets directly into your S3 bucket.  Make sure it is set
to be publicly readable.

```
andy@shoggoth:s3-static-site$ aws s3 cp index.html s3://foobie.testtest.aws.cowell.org/index.html --acl public-read
upload: ./index.html to s3://foobie.testtest.aws.cowell.org/index.html
```
