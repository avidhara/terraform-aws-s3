# Terraform module for AWS S3

## Prerequisites

- Terraform 0.12.x

### Use as a Module

```hcl
module "s3" {
  source        = "./"
  bucket        = "testbucket"
  acl           = "private"
  force_destroy = true

  tags = {
    Owner = "DevOps"
  }

  versioning = {
    enabled = true
  }
    server_side_encryption_configuration = {
    rule = {
      apply_server_side_encryption_by_default = {
        sse_algorithm     = "AES256"
      }
    }
  }
}
```

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| aws | n/a |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| acceleration\_status | (Optional) Sets the accelerate configuration of an existing bucket. Can be Enabled or Suspended. | `string` | `null` | no |
| acl | (Optional) The canned ACL to apply. Defaults to 'private'. | `string` | `"private"` | no |
| attach\_policy | Controls if S3 bucket should have bucket policy attached (set to `true` to use value of `policy` as bucket policy) | `bool` | `false` | no |
| block\_public\_acls | Whether Amazon S3 should block public ACLs for this bucket. | `bool` | `true` | no |
| block\_public\_policy | Whether Amazon S3 should block public bucket policies for this bucket. | `bool` | `true` | no |
| bucket | (Optional, Forces new resource) The name of the bucket. If omitted, Terraform will assign a random, unique name. | `string` | `null` | no |
| cors\_rule | Map containing a rule of Cross-Origin Resource Sharing. | `any` | `{}` | no |
| create\_bucket | if S3 bucket should be created set it to True, Default Sets to True | `bool` | `true` | no |
| force\_destroy | (Optional, Default:false ) A boolean that indicates all objects should be deleted from the bucket so that the bucket can be destroyed without error. These objects are not recoverable. | `bool` | `false` | no |
| ignore\_public\_acls | Whether Amazon S3 should ignore public ACLs for this bucket. | `bool` | `true` | no |
| lifecycle\_rule | List of maps containing configuration of object lifecycle management. | `any` | `[]` | no |
| logging | Map containing access bucket logging configuration. | `map(string)` | `{}` | no |
| object\_lock\_configuration | Map containing S3 object locking configuration. | `any` | `{}` | no |
| policy | (Optional) A valid bucket policy JSON document. Note that if the policy document is not specific enough (but still valid), Terraform may view the policy as constantly changing in a terraform plan. In this case, please make sure you use the verbose/specific version of the policy. For more information about building AWS IAM policy documents with Terraform, see the AWS IAM Policy Document Guide. | `string` | `null` | no |
| region | If specified, the AWS region this bucket should reside in. Otherwise, the region used by the callee. | `string` | `"us-west-2"` | no |
| replication\_configuration | Map containing cross-region replication configuration. | `any` | `{}` | no |
| request\_payer | (Optional) Specifies who should bear the cost of Amazon S3 data transfer. Can be either BucketOwner or Requester. By default, the owner of the S3 bucket would incur the costs of any data transfer. See Requester Pays Buckets developer guide for more information. | `string` | `null` | no |
| restrict\_public\_buckets | Whether Amazon S3 should restrict public bucket policies for this bucket. | `bool` | `true` | no |
| server\_side\_encryption\_configuration | Map containing server-side encryption configuration. | `any` | `{}` | no |
| tags | (Optional) A mapping of tags to assign to the bucket. | `map(string)` | `{}` | no |
| versioning | Map containing versioning configuration. | `map(string)` | `{}` | no |
| website | Map containing static web-site hosting or redirect configuration. | `map(string)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| arn | The ARN of the bucket. Will be of format arn:aws:s3:::bucketname. |
| bucket\_domain\_name | The bucket domain name. Will be of format bucketname.s3.amazonaws.com. |
| bucket\_regional\_domain\_name | The bucket region-specific domain name. The bucket domain name including the region name, please refer here for format. Note: The AWS CloudFront allows specifying S3 region-specific endpoint when creating S3 origin, it will prevent redirect issues from CloudFront to S3 Origin URL. |
| hosted\_zone\_id | The Route 53 Hosted Zone ID for this bucket's region. |
| id | The name of the bucket. |
| region | The AWS region this bucket resides in. |
| website\_domain | The domain of the website endpoint, if the bucket is configured with a website. If not, this will be an empty string. This is used to create Route 53 alias records. |
| website\_endpoint | The website endpoint, if the bucket is configured with a website. If not, this will be an empty string. |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
