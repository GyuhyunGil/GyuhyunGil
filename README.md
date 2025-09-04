# avogpt

## Prerequisites

- Install [Node.js](https://nodejs.org/en/download)
- Install [Yarn](https://yarnpkg.com/getting-started/install)
- Download [Docker](https://www.docker.com/products/docker-desktop) to run the database locally

## Getting Started

### avogpt-api

#### Go to the api folder

```sh
cd avogpt-api
```

#### Copy the environment variables

```sh
cp .env.example .env
```

fill some missing variables

- `PINECONE_NAMESPACE` - write your name or unique identifier to avoid conflicts with other developers

#### Run the database

```sh
docker run --name avogpt-pg -e POSTGRES_USER=avogpt -e POSTGRES_PASSWORD=asdf -p 5432:5432 -d postgres
```

#### Install the dependencies

```sh
yarn
```

#### Run the api

```sh
yarn dev
```

### avogpt-web

#### Go to the web folder

```sh
cd avogpt-web
```

#### Copy the environment variables

```sh
cp .env.example .env
```

#### Install the dependencies

```sh
yarn
```

#### Run the web

```sh
yarn dev
```

## AWS

AWS resources are listed below since we are not using any infrastructure as code tool yet.

### Resource Groups

- avogpt

### VPC

- avogpt-dev-vpc (10.16.0.0/16)
  - avogpt-dev-subnet-public1-us-west-2a
  - avogpt-dev-subnet-private1-us-west-2a
  - avogpt-dev-subnet-public2-us-west-2b
  - avogpt-dev-subnet-private2-us-west-2b
  - avogpt-dev-rtb-public
  - avogpt-dev-rtb-private1-us-west-2a
  - avogpt-dev-rtb-private2-us-west-2b
  - avogpt-dev-igw
  - avogpt-dev-vpce-s3
- avogpt-prod-vpc (10.0.0.0/16)
  - avogpt-prod-subnet-public1-us-west-2a
  - avogpt-prod-subnet-private1-us-west-2a
  - avogpt-prod-subnet-public2-us-west-2b
  - avogpt-prod-subnet-private2-us-west-2b
  - avogpt-prod-rtb-public
  - avogpt-prod-rtb-private1-us-west-2a
  - avogpt-prod-rtb-private2-us-west-2b
  - avogpt-prod-igw
  - avogpt-prod-vpce-s3

### S3

- avogpt-local
- avogpt-dev
- avogpt-prod

### RDS

- avogpt-dev (PostgreSQL)
  - avogpt-dev-rds-sg
  - avogpt-dev-rds-subnet-group
- avogpt-prod
  - avogpt-prod-rds-sg
  - avogpt-prod-rds-subnet-group

### ECR

- avogpt-dev
- avogpt-prod

### ECS

- avogpt-dev (Cluster)
  - avogpt-dev-api (Service)
    - avogpt-dev-api (Task Definition)
    - avogpt-dev-ecs-api-sg
- avogpt-prod
  - avogpt-prod-api
    - avogpt-prod-api
    - avogpt-prod-ecs-api-sg

`prod` uses private subnets and NAT gateway to access the internet while `dev` uses public subnets and internet gateway. This is because NAT gateway charges money.

### Load Balancer

- avogpt-dev-api
  - avogpt-dev-api (Target Group)
  - avogpt-dev-api-lb-sg
- avogpt-prod-api
  - avogpt-prod-api
  - avogpt-prod-api-lb-sg

### Route 53

- avogpt-dev-api (A Record of avomd.io)

### EC2

- avogpt-dev-bastion
  - avogpt-dev-bastion-sg
- avogpt-prod-bastion
  - avogpt-prod-bastion-sg

### IAM

#### Users

- avogpt-local-api
- avogpt-dev-api
- avogpt-prod-api
- avogpt-github-actions

#### Roles

- avogpt-dev-api-task-execution-role
- avogpt-prod-api-task-execution-role
