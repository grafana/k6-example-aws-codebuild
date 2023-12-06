# Automated k6 load testing with AWS CodeBuild CI/CD

This is an example repo for how to setup k6 with [AWS CodeBuild](https://aws.amazon.com/codebuild/) CI/CD to build load testing into an automation flow.

The full guide describing how to use this repository is located [here](https://k6.io/blog/integrating-k6-with-aws-codebuild/).

## Examples

| File                                                       | Description                        |
| ---------------------------------------------------------- | ---------------------------------- |
| [local-example/buildspec.yml](local-example/buildspec.yml) | Runs locally on AWS infrastructure |
| [cloud-example/buildspec.yml](cloud-example/buildspec.yml) | Runs on k6 cloud                   |

## Run Local

```bash
# Run locally
k6 run scripts/test.js

# Run via Docker
docker run -i grafana/k6 run - <scripts/test.js
```

## Run Cloud

```bash
# Run directly
k6 login cloud --token <YOUR_K6_CLOUD_API_TOKEN>
k6 cloud scripts/cloud-test.js

# Run via Docker
docker run -i -e K6_CLOUD_TOKEN=<API_TOKEN> grafana/k6 cloud - <scripts/cloud-test.js

# Alternative Docker version with mounting option
docker run -i -e K6_CLOUD_TOKEN=<API_TOKEN> -v "$PWD/scripts:/cloud-test.js" grafana/k6 cloud /cloud-test.js
```
