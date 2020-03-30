# AWS SQS Terraform module

A reusable module for creating AWS SQS queues, parameterising all options available. When creating a FIFO queue the module will automatically append '.fifo' to the name of the queue.

## Usage

```hcl
module "user_queue" {
  source  = "git::https://github.com/tom-murray/aws-sqs-terraform-module.git?ref=tags/1.0.0"

  name = "messaging"

  tags = {
    Service     = "messaging"
    Environment = "dev"
  }
}
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| content_based_deduplication | Enables content-based deduplication for FIFO queues | string | `false` | no |
| delay_seconds | The time in seconds that the delivery of all messages in the queue will be delayed. An integer from 0 to 900 (15 minutes) | string | `0` | no |
| fifo_queue | Boolean designating a FIFO queue | string | `false` | no |
| kms_data_key_reuse_period_seconds | The length of time, in seconds the key will be cached, to encrypt or decrypt messages before calling AWS KMS again. An integer representing seconds, between 60 seconds (1 minute) and 86,400 seconds (24 hours) | string | `300` | no |
| kms_master_key_id | The ID of an AWS-managed customer master key (CMK) string | `` | no |
| max_message_size | The limit of how many bytes a message can contain before Amazon SQS rejects it. An integer from 1024 bytes (1 KiB) up to 262144 bytes (256 KiB) | string | `262144` | no |
| message_retention_seconds | The number of seconds Amazon SQS retains a message. Integer representing seconds, from 60 (1 minute) to 1209600 (14 days) | string | `345600` | no |
| name | This is the name of the queue. If omitted, Terraform will assign a random name. | string | `` | no |
| policy | The JSON policy for the SQS queue | string | `` | no |
| receive_wait_time_seconds | The time for which a ReceiveMessage call will wait for a message to arrive (long polling) before returning. An integer from 0 to 20 (seconds) | string | `0` | no |
| redrive_policy | The JSON policy to set up the Dead Letter Queue, see AWS docs. Note: when specifying maxReceiveCount, you must specify it as an integer (5), and not a string ("5") | string | `` | no |
| tags | A mapping of tags to assign to all resources | string | `<map>` | no |
| visibility_timeout_seconds | The visibility timeout for the queue. An integer from 0 to 43200 (12 hours) | string | `30` | no |

## Outputs

| Name | Description |
|------|-------------|
| this_sqs_queue_name | The name of the SQS queue |
| this_sqs_queue_arn | The ARN of the SQS queue |
| this_sqs_queue_id | The URL for the created Amazon SQS queue |
