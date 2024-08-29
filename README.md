
# SonarQube Setup with Docker Compose

[![SonarQube](https://img.shields.io/badge/SonarQube-v9.9-blue)](https://www.sonarsource.com/products/sonarqube/)
[![Docker Compose](https://img.shields.io/badge/Docker%20Compose-v1.29.2-green)](https://docs.docker.com/compose/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A complete guide to setting up SonarQube using Docker Compose, designed for code quality and security checks in a CI/CD pipeline. This setup uses Docker Compose to orchestrate a SonarQube server and a PostgreSQL database, following best practices for deployment, security, and performance.

## Table of Contents

- [Introduction](#introduction)
- [Why Use SonarQube?](#why-use-sonarqube)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
  - [1. Clone the Repository](#1-clone-the-repository)
  - [2. Configure Environment Variables](#2-configure-environment-variables)
  - [3. Run Docker Compose](#3-run-docker-compose)
- [Advanced Configuration](#advanced-configuration)
- [Accessing SonarQube](#accessing-sonarqube)
- [System Requirements](#system-requirements)
- [Troubleshooting](#troubleshooting)
- [Resources](#resources)
- [Contributing](#contributing)
- [License](#license)

## Introduction

SonarQube is a powerful tool for continuous inspection of code quality and security. It performs static code analysis, providing detailed reports on code bugs, vulnerabilities, and code smells for over 25 programming languages. This project aims to simplify SonarQube setup and deployment using Docker Compose.

## Why Use SonarQube?

- **Code Quality**: Ensure code quality through continuous inspection and static analysis.
- **Security**: Identify vulnerabilities and security hotspots in your codebase.
- **Integrations**: Works seamlessly with CI/CD tools like Jenkins, GitHub Actions, Azure DevOps, and more.
- **Multi-Language Support**: Supports over 25 programming languages, making it ideal for polyglot environments.

## Prerequisites

Before you begin, make sure you have the following installed on your system:

- [Docker](https://www.docker.com/get-started) (version 20.10 or later)
- [Docker Compose](https://docs.docker.com/compose/install/) (version 1.29 or later)
- A Unix-based OS (Linux or macOS recommended) or WSL2 for Windows users.

## Installation

### 1. Clone the Repository

Clone this repository to your local machine:

```bash
git clone https://github.com/amrmarey/sonarqube.git
cd sonarqube
```

### 2. Configure Environment Variables

Configure the environment variables required for SonarQube and PostgreSQL by editing the `.env` file. The `.env` file should look like this:

```bash
# SonarQube Environment Variables
SONARQUBE_PORT=9000
SONAR_JDBC_URL=jdbc:postgresql://db:5432/sonarqube
SONAR_JDBC_USERNAME=sonarqube
SONAR_JDBC_PASSWORD=sonarqube

# PostgreSQL Environment Variables
POSTGRES_USER=sonarqube
POSTGRES_PASSWORD=sonarqube
POSTGRES_DB=sonarqube
```

### 3. Run Docker Compose

Start the SonarQube and PostgreSQL services using Docker Compose:

```bash
docker-compose up -d
```

This command will start both SonarQube and PostgreSQL containers in detached mode.

## Advanced Configuration

- **Persistent Volumes**: Ensure your data is not lost by configuring persistent Docker volumes for SonarQube's `data`, `extensions`, and `logs` directories.
- **Custom Plugins**: Install custom plugins by mounting a directory with plugins into the `/opt/sonarqube/extensions/plugins` volume.
- **Memory and Performance**: Adjust the SonarQube JVM options by setting the `SONARQUBE_WEB_JVM_OPTS` environment variable to optimize performance:
  ```bash
  SONARQUBE_WEB_JVM_OPTS="-Xmx512m -Xms128m"
  ```
- **Reverse Proxy Configuration**: For secure production deployment, configure a reverse proxy with HTTPS using Nginx, Apache, or Traefik.

## Accessing SonarQube

Once the containers are up and running, you can access the SonarQube web interface by navigating to [http://localhost:9000](http://localhost:9000) in your web browser.

- **Default Admin Credentials**:
  - Username: `admin`
  - Password: `admin`

After the first login, you will be prompted to change the default password.

## System Requirements

- **Memory**: Minimum 2GB RAM for SonarQube server. Additional memory may be required depending on the size of your project and number of users.
- **Storage**: Ensure adequate disk space for data and logs. Persistent volumes are recommended.
- **CPU**: Minimum 2 CPU cores are recommended for optimal performance.

## Troubleshooting

- **Permissions Issues**: Ensure that the mounted volumes have the correct permissions. If you encounter a `Permission denied` error, you may need to adjust the ownership or permissions of the volume directories on the host machine.
  
  ```bash
  sudo chown -R 1001:1001 sonarqube_data sonarqube_extensions sonarqube_logs
  ```

- **Port Conflicts**: Make sure port `9000` is not being used by another service on your host machine. You can change the port in the `.env` file if needed.

- **Database Connection Issues**: Ensure the PostgreSQL service is running and that the connection settings in the `.env` file are correct.

## Resources

- [SonarQube Official Documentation](https://docs.sonarsource.com/sonarqube/latest/)
- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request or open an issue for any bugs, improvements, or features you'd like to see.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

---

For any questions, feel free to reach out to [amr.marey@msn.com](mailto:amr.marey@msn.com).
