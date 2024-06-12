# Terraform Cloud Getting Started Guide Example

This is an example Terraform configuration intended for use with the [Terraform Cloud Getting Started Guide](https://learn.hashicorp.com/terraform/cloud-gettingstarted/tfc_overview).

## What will this do?

This is a Terraform configuration that will create an EC2 instance in your AWS account. 

When you set up a Workspace on Terraform Cloud, you can link to this repository. Terraform Cloud can then run `terraform plan` and `terraform apply` automatically when changes are pushed. For more information on how Terraform Cloud interacts with Version Control Systems, see [our VCS documentation](https://www.terraform.io/docs/cloud/run/ui.html).

## What are the prerequisites?

You must have an AWS account and provide your AWS Access Key ID and AWS Secret Access Key to Terraform Cloud. Terraform Cloud encrypts and stores variables using [Vault](https://www.vaultproject.io/). For more information on how to store variables in Terraform Cloud, see [our variable documentation](https://www.terraform.io/docs/cloud/workspaces/variables.html).

The values for `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` should be saved as environment variables on your workspace.


https://marketplace.visualstudio.com/_apis/public/gallery/publishers/HashiCorp/vsextensions/terraform/2.27.2023071109/vspackage?targetPlatform=win32-x64



https://marketplace.visualstudio.com/items?itemName=HashiCorp.terraform


Terraform Extension for Visual Studio Code
The HashiCorp Terraform Extension for Visual Studio Code (VS Code) with the Terraform Language Server adds editing features for Terraform files such as syntax highlighting, IntelliSense, code navigation, code formatting, module explorer and much more!

Quick Start
Get started writing Terraform configurations with VS Code in three steps:

Step 1: If you haven't done so already, install Terraform

Step 2: Install the Terraform Extension for VS Code.

Step 3: To activate the extension, open any folder or VS Code workspace containing Terraform files. Once activated, the Terraform language indicator will appear in the bottom right corner of the window.

New to Terraform? Read the Terraform Learning guides

See Usage for more detailed getting started information.

Read the Troubleshooting Guide for answers to common questions.

Features
IntelliSense Edit your code with auto-completion of providers, resource names, data sources, attributes and more
Syntax validation Diagnostics using terraform validate provide inline error checking
Syntax highlighting Highlighting syntax from Terraform 0.12 to 1.X
Code Navigation Navigate through your codebase with Go to Definition and Symbol support
Code Formatting Format your code with terraform fmt automatically
Code Snippets Shortcuts for common snippets like for_each and variable
Terraform Cloud Integration View Terraform Cloud Workspaces and Run details inside VS Code
Terraform Module Explorer View all modules and providers referenced in the currently open document.
Terraform commands Directly execute commands like terraform init or terraform plan from the VS Code Command Palette.
IntelliSense and Autocomplete
IntelliSense is a general term for a variety of code editing features including: code completion, parameter info, quick info, and member lists. IntelliSense features are sometimes called by other names such as autocomplete, code completion, and code hinting.

For Terraform constructs like resource and data, labels, blocks and attributes are auto completed both at the root of the document and inside other blocks. This also works for Terraform modules that are installed in the workspace, attributes and other constructs are autocompleted.

Note: If there are syntax errors present in the document upon opening, intellisense may not provide all completions. Please fix the errors and reload the document and intellisense will return. See hcl-lang#57 for more information.

Invoking intellisense is performed through the keyboard combination for your platform and the results depend on where the cursor is placed.

If the cursor is at the beginning of a line and no other characters are present, then a list of constructs like data, provider, resource, etc are shown.




















```

# Initialize S3 client
s3 = boto3.client(
    's3',
    aws_access_key_id=aws_access_key,
    aws_secret_access_key=aws_secret_access_key,
    endpoint_url=endpoint_url,
    config=Config(signature_version='s3v4'),
    verify=False
)

def check_bucket_exists():
    try:
        s3.head_bucket(Bucket=bucket_name)
        print(f'Bucket "{bucket_name}" exists.')
        return True
    except Exception as e:
        print(f'Bucket "{bucket_name}" does not exist: {e}')
        return False

def check_object_exists(key):
    try:
        s3.head_object(Bucket=bucket_name, Key=key)
        print(f'Object "{key}" exists in bucket "{bucket_name}".')
        return True
    except Exception as e:
        print(f'Object "{key}" does not exist: {e}')
        return False

def create_test_file():
    try:
        response = s3.put_object(
            Bucket=bucket_name,
            Key=f'{test_folder}/{test_file_name}',
            Body=test_file_content
        )
        print(f'Test file created successfully: {response}')
    except Exception as e:
        print(f'Error creating test file: {e}')

def read_test_file():
    try:
        response = s3.get_object(
            Bucket=bucket_name,
            Key=f'{test_folder}/{test_file_name}'
        )
        content = response['Body'].read().decode('utf-8')
        print(f'Test file content: {content}')
    except Exception as e:
        print(f'Error reading test file: {e}')

def delete_test_file():
    try:
        response = s3.delete_object(
            Bucket=bucket_name,
            Key=f'{test_folder}/{test_file_name}'
        )
        print(f'Test file deleted successfully: {response}')
    except Exception as e:
        print(f'Error deleting test file: {e}')

def list_files_in_folder():
    try:
        response = s3.list_objects_v2(
            Bucket=bucket_name,
            Prefix=f'{test_folder}/'
        )
        if 'Contents' in response:
            files = [obj['Key'] for obj in response['Contents']]
            print('Files in folder:')
            for file in files:
                print(file)
        else:
            print('No files found in the folder.')
    except Exception as e:
        print(f'Error listing files: {e}')

def copy_test_file():
    try:
        if check_object_exists(f'{test_folder}/{test_file_name}'):
            copy_source = {'Bucket': bucket_name, 'Key': f'{test_folder}/{test_file_name}'}
            s3.copy_object(CopySource=copy_source, Bucket=bucket_name, Key=f'{test_folder}/copy_{test_file_name}')
            print('Test file copied successfully.')
    except Exception as e:
        print(f'Error copying test file: {e}')

def move_test_file():
    try:
        copy_test_file()
        delete_test_file()
        print('Test file moved successfully.')
    except Exception as e:
        print(f'Error moving test file: {e}')

def download_test_file():
    try:
        if check_object_exists(f'{test_folder}/{test_file_name}'):
            s3.download_file(bucket_name, f'{test_folder}/{test_file_name}', local_download_path)
            print(f'Test file downloaded successfully to {local_download_path}.')
    except Exception as e:
        print(f'Error downloading test file: {e}')

def upload_large_file():
    large_file_path = 'large_test_file.txt'
    try:
        # Create a large file for testing
        with open(large_file_path, 'w') as f:
            f.write('A' * 10 * 1024 * 1024)  # 10MB file

        s3.upload_file(large_file_path, bucket_name, f'{test_folder}/large_test_file.txt')
        print('Large test file uploaded successfully.')
    except Exception as e:
        print(f'Error uploading large test file: {e}')
    finally:
        if os.path.exists(large_file_path):
            os.remove(large_file_path)

if __name__ == '__main__':
    if check_bucket_exists():
        print('Creating test file...')
        create_test_file()

        print('Reading test file...')
        read_test_file()

        print('Listing files in folder...')
        list_files_in_folder()

        print('Copying test file...')
        copy_test_file()

        print('Downloading test file...')
        download_test_file()

        print('Uploading large file...')
        upload_large_file()

        print('Deleting test file...')
        delete_test_file()

        print('Listing files in folder again...')
        list_files_in_folder()


```
