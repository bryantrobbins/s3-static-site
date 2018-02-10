# S3 Static Site

An AWS CloudFormation template to build an S3 static website behind a Cloudfront
distribution.

## Requirements

You need an existing Route53 Hosted Zone to reference, as well as the ARN for an
existing ACM certificate that matches the domain you want.  It can be a wildcard
cert.

## Parameters

* **SiteHostName**: The "hostname" portion of the URL for the S3 Static Site you are
creating.  For example, if you were creating the site www.example.com, the
hostname portion is www.
* **SiteDomainName**: The "domain name" portion of the URL for the S3 Static Site you
are creating.  For example, if you were creating the site\nwww.example.com,
the domain name portion is example.com.  The domain\nname should NOT end in
a period.
* **CertArn**: The ARN for the ACM Certificate to be used on this site's Cloudfront
distribution.

## Launching Stack

The stack build will take 30+ minutes, due to the length of time Cloudfront takes to
provision.

```
% aws cloudformation create-stack --stack-name example-stack \
  --template-body file://s3-static-site.yaml \
  --parameters
      ParameterKey=SiteHostName,ParameterValue=test
      ParameterKey=SiteDomainName,ParameterValue=ratemytank.com
      ParameterKey=CertArn,ParameterValue=arn:aws:acm:us-east-1:123456789012:certificate/a3340aab-b529-43a7-a7f9-fca74b6b009a
```
