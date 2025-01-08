 Hi there 👋


```markdown
 Reverse Proxy and Load Balancer Project

 Description
This project demonstrates the setup of a Reverse Proxy and Load Balancer system using 5 Ubuntu virtual machines (VMs). The primary goal is to distribute traffic efficiently across multiple backend servers to ensure high availability and load balancing. Nginx is used as a Reverse Proxy and Load Balancer, while Apache is used for handling the backend API requests.

 Installation

 Prerequisites
Before proceeding, ensure the following software is installed on all VMs:
- Ubuntu 20.04 or later
- Nginx (for Reverse Proxy and Load Balancer)
- Apache2 (for backend API handling)
- PHP and MySQL (on backend servers)

 Steps to Install

1. **Set up the 5 Ubuntu VMs**:
   - VM1: Nginx Reverse Proxy (IP: 192.168.100.1)
   - VM2: Backend Server 1 (Apache) (IP: 192.168.100.2)
   - VM3: Backend Server 2 (Apache) (IP: 192.168.100.3)
   - VM4: Database Server (MySQL) (IP: 192.168.100.4)
   - VM5: Monitoring Server (IP: 192.168.100.5)

2. **Install Nginx on the Reverse Proxy VM (VM1)**:
   ```
   sudo apt update
   sudo apt install nginx
   ```

3. **Configure Nginx as a Reverse Proxy and Load Balancer**:
   - Edit the `/etc/nginx/sites-available/default` file to configure upstream servers and load balancing.
   - Example configuration for load balancing:
     ```nginx
     upstream backend {
         server 192.168.100.2;
         server 192.168.100.3;
     }

     server {
         listen 80;

         location / {
             proxy_pass http://backend;
             proxy_set_header Host $host;
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
         }
     }
     ```

4. **Install Apache2 on Backend VMs (VM2 and VM3)**:
   ```
   sudo apt update
   sudo apt install apache2
   ```

5. **Install MySQL on the Database VM (VM4)**:
   ```
   sudo apt update
   sudo apt install mysql-server
   ```

6. **Configure Database Connections**:
   - Set up a MySQL database and user on VM4 for backend APIs.

7. **Test the Setup**:
   - Ensure that Nginx is correctly forwarding requests to the backend Apache servers.
   - Ensure that MySQL is accessible by the backend servers.

 Usage

1. **Accessing the Reverse Proxy**:
   - Once the setup is complete, you can access the load-balanced application via the IP address of the Reverse Proxy VM (192.168.100.1).

2. **Adding More Backend Servers**:
   - You can scale the backend by adding more Apache servers to the `upstream` block in the Nginx configuration.

 Examples

1. **Example of Load Balancing with Nginx**:
   - Nginx will distribute incoming requests between the backend servers (VM2 and VM3) using a round-robin method.

2. **Example of Database Access**:
   - The backend servers (VM2 and VM3) will connect to the MySQL database on VM4 to fetch or store data.

 Testing

1. **Test Nginx Load Balancing**:
   - You can test load balancing by sending multiple HTTP requests to the Reverse Proxy VM (192.168.100.1) and verifying that traffic is balanced across backend servers (VM2 and VM3).

2. **Test Database Connectivity**:
   - Ensure that the backend servers can connect to MySQL on VM4 by running queries via PHP or MySQL client tools.

 Contributing

Contributions to improve the configuration and performance of the reverse proxy and load balancing setup are welcome. To contribute:
1. Fork the repository.
2. Create a new branch.
3. Make your changes and commit them.
4. Open a pull request.

 License


 Contact Information

For any issues or questions, you can contact the project maintainer at: saengsaichaiyo@gmail.con .
```

