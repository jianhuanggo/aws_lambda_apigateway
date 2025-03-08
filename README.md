# AWS Lambda API Gateway Integration

This project provides a production-grade Python implementation for integrating AWS API Gateway with Lambda functions using the boto3 SDK.

## Overview

This package allows you to:
1. Create and configure API Gateway endpoints
2. Connect API Gateway endpoints to Lambda functions
3. Make REST calls to execute Lambda functions and retrieve results

## Installation

```bash
pip install -r requirements.txt
```

## Configuration

Create a `.env` file based on the `.env.example` template and add your AWS credentials:

```
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=us-east-1
API_GATEWAY_ID=5321hipmwk
LAMBDA_FUNCTION_NAME=lambda-pg_api_metadata
```

## Usage

### Basic Usage

```python
from src.api_gateway_lambda.api_gateway_manager import ApiGatewayManager

# Initialize the manager
api_manager = ApiGatewayManager()

# Create an API Gateway endpoint connected to a Lambda function
api_id, invoke_url = api_manager.create_or_update_api_gateway(
    api_name="MyAPI",
    resource_path="my-resource",
    http_method="GET"
)

print(f"API Gateway endpoint URL: {invoke_url}")
```

### Calling the API Gateway Endpoint

```python
from src.api_gateway_lambda.api_client import ApiClient

# Initialize the client
api_client = ApiClient()

# Make a request to the API Gateway endpoint
response = api_client.make_request(
    url="https://your-api-id.execute-api.us-east-1.amazonaws.com/prod/my-resource",
    method="GET"
)

print(f"Response: {response}")
```

### Direct Lambda Invocation

```python
from src.api_gateway_lambda.lambda_client import LambdaClient

# Initialize the client
lambda_client = LambdaClient()

# Invoke the Lambda function directly
response = lambda_client.invoke_lambda(
    payload={"key": "value"}
)

print(f"Response: {response}")
```

## Examples

The `examples` directory contains several scripts demonstrating different aspects of the package:

- `create_api_gateway.py`: Creates an API Gateway endpoint integrated with a Lambda function
- `invoke_lambda.py`: Invokes a Lambda function directly
- `call_api_gateway.py`: Makes a request to an API Gateway endpoint
- `complete_example.py`: Demonstrates the full workflow from creation to invocation
- `advanced_example.py`: Showcases advanced features including multiple resources, HTTP methods, error handling, and parallel requests

To run an example:

```bash
cd examples
python create_api_gateway.py
```

## Testing

Run the tests with pytest:

```bash
pytest
```

For more detailed test output:

```bash
pytest -v
```

To generate a coverage report:

```bash
coverage run -m pytest
coverage report
```

## Project Structure

```
aws_lambda_apigateway/
├── .env.example           # Example environment variables
├── .gitignore             # Git ignore file
├── README.md              # Project documentation
├── requirements.txt       # Project dependencies
├── setup.py               # Package setup file
├── src/                   # Source code
│   └── api_gateway_lambda/
│       ├── __init__.py
│       ├── api_client.py          # Client for making API requests
│       ├── api_gateway_manager.py # Manager for API Gateway operations
│       ├── config.py              # Configuration module
│       └── lambda_client.py       # Client for Lambda operations
├── tests/                 # Unit tests
│   ├── __init__.py
│   ├── conftest.py               # Pytest configuration
│   ├── test_api_client.py        # Tests for ApiClient
│   ├── test_api_gateway_manager.py # Tests for ApiGatewayManager
│   ├── test_config.py            # Tests for Config
│   └── test_lambda_client.py     # Tests for LambdaClient
└── examples/              # Example scripts
    ├── call_api_gateway.py       # Example of calling an API Gateway
    ├── complete_example.py       # Complete workflow example
    ├── create_api_gateway.py     # Example of creating an API Gateway
    └── invoke_lambda.py          # Example of invoking a Lambda function
```

## License

MIT
