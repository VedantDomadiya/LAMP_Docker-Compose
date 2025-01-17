# Setting Up a LAMP Server with Docker Compose

This guide provides a step-by-step approach to setting up a **LAMP (Linux, Apache, MySQL, PHP)** server using Docker containers.

---

## 🚀 What is a LAMP Stack?

A **LAMP stack** is a popular web service stack comprising:

- **Linux**: Operating system  
- **Apache**: Web server  
- **MySQL**: Database management system  
- **PHP**: Scripting language  

With Docker, we containerize these components for a consistent, reliable, and scalable environment.

---

## 🌟 Why Use Docker for LAMP?

Docker simplifies LAMP deployment by offering:
- **Environment Isolation**: No conflicts between dependencies.  
- **Easy Scalability**: Lightweight, portable containers.  
- **Simplified Management**: Unified control via Docker commands.

---

## 🛠️ Prerequisites

Ensure you have:
1. **Linux-based system** (e.g., Ubuntu 22.04).  
2. **Docker** and **Docker Compose** installed.  

To install Docker:  
```bash
sudo apt update
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker
```

To install Docker Compose:  
```bash
sudo apt install docker-compose
```

---

## 📝 Step 1: Define `docker-compose.yml`

Create a `docker-compose.yml` file with the following content:

```yaml
version: '3'

services:
  web:
    image: php:7.4-apache
    container_name: lamp_web
    volumes:
      - ./html:/var/www/html
    ports:
      - "8080:80"
    networks:
      - lamp-network

  db:
    image: mysql:5.7
    container_name: lamp_db
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: mydb
      MYSQL_USER: user
      MYSQL_PASSWORD: userpassword
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - lamp-network

networks:
  lamp-network:

volumes:
  db_data:
```

### Configuration Breakdown:
- **PHP & Apache**: Official `php:7.4-apache` image serving files from `./html`.  
- **MySQL**: `mysql:5.7` with defined credentials.  
- **Networking & Volumes**: Custom `lamp-network` and `db_data` volume for persistence.

---

## 📂 Step 2: Set Up Directory Structure

1. Create a project directory:
   ```bash
   mkdir lamp_docker && cd lamp_docker
   mkdir html
   ```
2. Add a simple `index.php` file to the `html` folder:
   ```php
   <?php
   phpinfo();
   ?>
   ```

---

## ▶️ Step 3: Run the Docker Containers

Start the LAMP stack:  
```bash
docker-compose up -d
```

Visit `http://localhost:8080` in your browser. You should see the **PHP Info** page.

---

## 🛢️ Step 4: Access the MySQL Database

Connect to MySQL from the terminal:  
```bash
docker exec -it lamp_db mysql -uuser -p
```

---

## ⏸️ Step 5: Manage Containers

- Stop and remove containers:  
  ```bash
  docker-compose down
  ```
- Stop containers without removing them:  
  ```bash
  docker-compose stop
  ```

---

## 📈 Step 6: Scale the LAMP Stack

To scale services (e.g., 3 web server instances):  
```yaml
web:
  image: php:7.4-apache
  deploy:
    replicas: 3
```

For advanced scalability, consider **Docker Swarm** or **Kubernetes**.

---

## 🔒 Step 7: Secure Your LAMP Stack

### Best Practices:
1. **Use SSL**: Encrypt data using Let's Encrypt:  
   ```bash
   sudo apt install certbot python3-certbot-apache
   sudo certbot --apache
   ```
2. **Secure MySQL**: Use strong passwords and IP restrictions.  
3. **Harden PHP**: Disable dangerous functions (`exec()`, `shell_exec()`) in `php.ini`.  

---

## 🎯 Conclusion

By containerizing the LAMP stack with Docker, you gain:
- A **scalable** and **isolated** development environment.  
- Reduced dependency conflicts.  
- Streamlined deployment processes.

With minimal setup, your LAMP stack is ready to support web applications for both development and production.

--- 

Feel free to clone this project and adapt it to your needs! 🎉

--- 

### 📎 Useful Commands:
- Start services:  
  ```bash
  docker-compose up -d
  ```
- Stop services:  
  ```bash
  docker-compose down
  ```
- Access MySQL:  
  ```bash
  docker exec -it lamp_db mysql -uuser -p
  ```

--- 

### 🙌 Feedback & Contributions
Contributions and suggestions are welcome! Open an issue or submit a pull request.

---


