# Expense Management Project

## Overview
This project is an expense management system consisting of three main components:
1. **Database (MySQL)**
2. **Backend (Node.js)**
3. **Frontend (Nginx)**

The project is designed to be deployed automatically using the provided bash scripts (`mysql.sh`, `backend.sh`, and `frontend.sh`). These scripts handle the installation, configuration, and startup of each component, ensuring a smooth and repeatable setup.

## Prerequisites
- A Linux environment with `dnf` package manager (e.g., CentOS, RHEL, or Fedora).
- Root or sudo access.
- Internet connection to download required packages and files.

## Scripts

### 1. `mysql.sh` (Database Setup)
This script installs and configures a MySQL server. It also checks whether the MySQL root password is already set, ensuring idempotency.

**Steps:**
1. Installs MySQL server.
2. Enables and starts the MySQL service.
3. Prompts for MySQL root password.
4. Verifies if the root password has been set or not, and sets it if necessary.

**Usage:**
```bash
sudo ./mysql.sh
```

### 2. `backend.sh` (Node.js Backend Setup)
This script sets up the Node.js backend for the expense management application. It installs Node.js, downloads the backend code, and configures it as a system service.

**Steps:**
1. Disables the default `nodejs` module and enables Node.js version 20.
2. Installs Node.js and creates a user `expense` (if not already created).
3. Downloads and unzips the backend code into `/app`.
4. Installs Node.js dependencies using `npm`.
5. Configures and starts the backend as a service using `systemd`.
6. Loads the MySQL schema into the database.

**Usage:**
```bash
sudo ./backend.sh
```

### 3. `frontend.sh` (Nginx Frontend Setup)
This script installs Nginx and sets up the frontend for the expense management system by downloading and configuring the frontend code.

**Steps:**
1. Installs Nginx.
2. Removes any existing content from the Nginx web directory.
3. Downloads and unzips the frontend code into `/usr/share/nginx/html`.
4. Copies the custom Nginx configuration for the expense app.
5. Restarts the Nginx service.

**Usage:**
```bash
sudo ./frontend.sh
```

## MySQL Connection
The scripts assume that the MySQL server is hosted at `db.daws78s.online`. You will need the MySQL root password to connect and load the database schema.

## System Services
- **Backend**: The backend service will be installed as a `systemd` service, allowing you to manage it using `systemctl` commands:
  - Start: `sudo systemctl start backend`
  - Enable: `sudo systemctl enable backend`
  - Status: `sudo systemctl status backend`

- **Frontend**: The frontend will be served by Nginx, which you can manage similarly:
  - Start: `sudo systemctl start nginx`
  - Enable: `sudo systemctl enable nginx`
  - Status: `sudo systemctl status nginx`

## Logs
Each script logs its operations into `/tmp/{script_name}-{timestamp}.log` for debugging purposes.
