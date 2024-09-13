# AWS Lambda S3 Logger

This project demonstrates an AWS Lambda function that:

1. **Is Invoked Every Minute**: The Lambda function is triggered every minute using EventBridge.
2. **Uses `boto3` Layer**: The function utilizes a `boto3` layer prepared on an Ubuntu instance using Ansible.
3. **Writes to S3 Bucket**: It creates a new file in an S3 bucket with the current datetime and the content `"I wrote it at $date"`.
4. **Uses Environment Variable**: Configured to use an environment variable for the S3 bucket name.

## Architecture

- **Terraform**: Manages the creation and configuration of AWS resources such as the Lambda function, EventBridge rule, and S3 bucket.
- **Ansible**: Used to prepare the environment on an Ubuntu instance by installing the `boto3` library.
- **Docker**: Builds and pushes the Lambda function image to Amazon ECR.
- **Lambda Function**: Executes every minute and writes a file to the S3 bucket.
- **EventBridge Scheduler**: Triggers the Lambda function every minute.
- **S3 Bucket**: Stores the files created by the Lambda function.

## Setup Instructions

### 1. **Prepare Infrastructure with Terraform**

1. **Define the Infrastructure**: Use Terraform to create and configure the necessary AWS resources including the Lambda function, EventBridge rule, and S3 bucket.
2. **Apply Configuration**: Initialize and apply the Terraform configuration to set up the infrastructure.

### 2. **Prepare the `boto3` Layer with Ansible**

1. **Create an Ansible Playbook**: Prepare an Ansible playbook to install the `boto3` library on an Ubuntu instance.
2. **Run the Playbook**: Execute the playbook to ensure `boto3` is available in your environment.

### 3. **Build and Push Lambda Function Image to ECR**

1. **Create a Dockerfile**: Define the Dockerfile for your Lambda function, specifying the base image and copying the Lambda function code.
2. **Build and Tag Docker Image**: Build the Docker image and tag it for ECR.
3. **Push Docker Image**: Push the tagged Docker image to your Amazon ECR repository.

### 4. **Verify the Setup**

- **Lambda Function Execution**: Monitor CloudWatch Logs to confirm that the Lambda function is executing every minute as expected.
- **S3 Bucket**: Check the S3 bucket to ensure that new files are being created with the correct content.

## Notes

- Ensure that your Lambda function’s IAM role has the required permissions to write to the S3 bucket.
- Confirm that the `boto3` layer is correctly prepared and accessible.
- Verify that the Lambda function configuration is correctly set to use the ECR image.

## License

This project is licensed under the [MIT License](LICENSE).
