# Code

## Navigation
- [Introduction](#introduction)
- [Use Cases](#use-cases)
- [Local Deployment](#local-deployment)
- [Security Policy](#security-policy)

## Introduction

The code node supports the execution of Python / NodeJS code to perform data transformations within workflows. It simplifies your workflows, suitable for Arithmetic, JSON transform, text processing, and more scenarios.

This node significantly enhances developers' flexibility, allowing them to embed custom Python or Javascript scripts in their workflows and manipulate variables in ways that preset nodes cannot achieve. Through configuration options, you can specify the required input and output variables and write the corresponding execution code:

<figure><img src="../../../.gitbook/assets/image (157).png" alt="" width="375"><figcaption></figcaption></figure>

## Configuration
If you need to use variables from other nodes within the code node, you need to define the variable names in `input variables` and reference these variables, see [Variable Reference](../key_concept.md#variable) for details.

## Use Cases
With the code node, you can perform the following common operations:

### Structured Data Processing
In workflows, it's often necessary to deal with unstructured data processing, such as parsing, extracting, and transforming JSON strings. A typical example is data processing in the HTTP node, where data might be nested within multiple layers of JSON objects, and we need to extract certain fields. The code node can help you accomplish these tasks. Here's a simple example that extracts the `data.name` field from a JSON string returned by an HTTP node:

```python
def main(http_response: str) -> str:
    import json
    data = json.loads(http_response)
    return data['data']['name']
```

### Mathematical Calculations
When complex mathematical calculations are needed in workflows, the code node can also be used. For example, to calculate a complex mathematical formula or perform some statistical analysis on the data. Here is a simple example that calculates the variance of a list:

```python
def main(x: list) -> float:
    return sum([(i - sum(x) / len(x)) ** 2 for i in x]) / len(x)
```

### Data Concatenation

```python
def main(knowledge1: list, knowledge2: list) -> list:
    return knowledge1 + knowledge2
```

## Local Deployment
f you are a user deploying locally, you need to start a sandbox service, which ensures that malicious code is not executed. Also, launching this service requires Docker, and you can find specific information about the Sandbox service [here](https://github.com/langgenius/dify/tree/main/docker/docker-compose.middleware.yaml). You can also directly start the service using docker-compose
```bash
docker-compose -f docker-compose.middleware.yaml up -d
```

## Security Policy
The execution environment is sandboxed for both Python and Javascript, meaning that certain functionalities that require extensive system resources or pose security risks are not available. This includes, but is not limited to, direct file system access, network calls, and operating system-level commands.
