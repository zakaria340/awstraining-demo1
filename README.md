# AWS Training ECR/ECS demo1

This project is a simple Node.js application exposing resources via `/api/items`. It is used for training on Docker and AWS ECR/ECS

## Prerequisites

Before getting started, make sure you have installed:

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)
- An AWS account with access to ECR/ECS

## Installation and Running

1. **Clone the repository**
   ```sh
   git clone <REPO_URL>
   cd <REPO_NAME>
   ```

2. **Build and run the container**
   ```sh
   docker-compose up -d
   ```

3. **Access the API**
   The API will be available at: [http://localhost:3000/api/items](http://localhost:3000/api/items)

    ### Get all items
        curl http://localhost:3000/api/items

    ### Create a new item
        curl -X POST -H "Content-Type: application/json" -d '{"name":"New Item","description":"Description of new item"}' http://localhost:3000/api/items

## Deployment on AWS ECR

1. **Login to AWS ECR**
   ```sh
   aws ecr get-login-password --region <REGION> | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.<REGION>.amazonaws.com
   ```

2. **Create an ECR repository**
   ```sh
   aws ecr create-repository --repository-name my-node-project
   ```

3. **Build and tag the Docker image**
   ```sh
   docker build -t demo1 .
   docker tag my-node-project:latest <AWS_ACCOUNT_ID>.dkr.ecr.<REGION>.amazonaws.com/my-node-project:latest
   ```

4. **Push the image to ECR**
   ```sh
   docker push <AWS_ACCOUNT_ID>.dkr.ecr.<REGION>.amazonaws.com/my-node-project:latest
   ```
   
### FIX timstamp Ubuntu
sudo ntpdate -u time.google.com

## License

This project is licensed under the MIT License.