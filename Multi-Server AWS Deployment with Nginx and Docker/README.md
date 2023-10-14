# Multi-Server AWS Deployment with NGINX and Docker

This project demonstrates a multi-server setup on AWS, consisting of three servers: two in a public subnet and one in a private subnet. The configuration includes a PostgreSQL database on the private server, an Nginx server with Docker on a public server, and two containers (frontend and backend) on another public server.

![Diagram](https://github.com/maaaruf/AWS-Infrastructure-Provisioning/blob/main/Multi-Server%20AWS%20Deployment%20with%20Nginx%20and%20Docker/diagrams/Multi-Server%20AWS%20Deployment%20with%20NGINX%20and%20Docker%20diagram.png)

## Contents

1. [Overview](#overview)
2. [Setup](#setup)
3. [Configuration](#configuration)
4. [Usage](#usage)
5. [Access URLs](#access-urls)
6. [Contributing](#contributing)
7. [License](#license)

---

## Overview

This project aims to showcase a real-world scenario involving the deployment of various services on AWS. It includes the following components:

- PostgreSQL database running on a server in a private subnet.
- Nginx server with Docker deployed on a server in a public subnet.
- Two containers - one for the frontend (React) and the other for the backend (Python or Node.js) - running on a separate public server.

## Setup

To replicate this setup, you'll need:

- Three AWS EC2 instances (2 in public subnet, 1 in private subnet).
- Properly configured VPC with public and private subnets.
- Security groups and routing tables appropriately set up.

## Configuration

1. **PostgreSQL Setup**: Configure the private server with PostgreSQL.
2. **Nginx Configuration**:

   - Install Docker and set up Nginx with Docker on the public server.
   - Create an Nginx configuration file to route requests to the respective containers based on the subdomain.
```js
upstream backend {
    server 192.168.0.4:80;
}

upstream frontend {
    server 192.168.0.5:80;
}

server {
    listen 80;
    server_name students.poridhi.com;

    location / {
        proxy_pass http://frontend;
    }
}

server {
    listen 80;
    server_name api.students.poridhi.com;

    location / {
        proxy_pass http://backend;
    }
}
```

3. **Container Deployment**:

   - Set up Docker on the public server hosting frontend and backend containers.
   - Deploy the respective containers.

## Usage

Once everything is set up, you can start using the application.

## Access URLs

- For frontend access: [http://students.poridhi.com](http://students.poridhi.com)
- For backend access: [http://api.students.poridhi.com](http://api.students.poridhi.com)

## Contributing

If you'd like to contribute to this project, create a pull request here. We welcome improvements to the project's setup and configurations.

## License

This project is licensed under the [MIT License](LICENSE). Feel free to use the code and resources here for your own learning and projects.

---

Happy coding!
