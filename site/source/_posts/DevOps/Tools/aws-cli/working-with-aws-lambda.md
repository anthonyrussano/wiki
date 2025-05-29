---
title: Working With AWS Lambda
image: lambda.png
tags:
- Tutorial
- Windows
- Powershell
---
Here are PowerShell AWS Lambda CLI commands:

```powershell
# List functions
aws lambda list-functions

# Get function details
aws lambda get-function --function-name FunctionName

# Create function
aws lambda create-function `
  --function-name FunctionName `
  --runtime python3.9 `
  --role RoleARN `
  --handler file.handler `
  --zip-file fileb://function.zip

# Update code
aws lambda update-function-code `
  --function-name FunctionName `
  --zip-file fileb://function.zip

# Invoke function
aws lambda invoke `
  --function-name FunctionName `
  --payload '{"key":"value"}' `
  output.txt

# Delete function
aws lambda delete-function --function-name FunctionName
```

Get a list of Lambda Names

```powershell
aws lambda list-functions --query 'Functions[*].FunctionName'
```

Check last execution times of functions:

```powershell
aws lambda list-functions --query 'Functions[*].[FunctionName,LastModified]' --output table
```

Or for more details including last execution:
```powershell
aws lambda list-functions --query 'Functions[*].[FunctionName,LastModified,LastUpdateStatus]' --output table
```

Get the Function Code

```powershell
# Get function code and configuration
aws lambda get-function --function-name FunctionName

# See just the function code
aws lambda get-function --function-name FunctionName --query 'Code.Location'

# Download the function code
Invoke-WebRequest -Uri (aws lambda get-function --function-name FunctionName --query 'Code.Location' --output text) -OutFile function.zip
```

After downloading, you can unzip to see the actual code.


How to invoke a lambda function:

```powershell
# Test with sample payload
aws lambda invoke --function-name FunctionName --payload '{"key":"value"}' output.txt

# Test without payload
aws lambda invoke --function-name FunctionName output.txt

# View output
Get-Content output.txt

# Test with specific event payload from file
aws lambda invoke --function-name FunctionName --payload file://event.json output.txt
```