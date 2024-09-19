# Gens.Life Platform

![Gens.Life Logo](https://drive.google.com/file/d/17Rql3OXy0VBNchzxb1eizOp1NUZu1zN5/view?usp=sharing)

## Table of Contents
1. [Project Overview](#project-overview)
2. [Key Features](#key-features)
3. [Technology Stack](#technology-stack)
4. [Hosting Environment](#hosting-environment)
5. [Domain Information](#domain-information)
6. [File Structure](#file-structure)
7. [Docker Compose Configuration](#docker-compose-configuration)
8. [Getting Started](#getting-started)
9. [Contributing](#contributing)
10. [License](#license)

## Project Overview

Gens.Life is an innovative online platform and real-world community dedicated to enhancing the lives of individuals aged 60 and above. Our mission is to create a safe and inclusive environment where seniors can connect, share experiences, and access resources that empower them to lead fulfilling lives.

The platform serves as a comprehensive hub for information, support, and community engagement tailored specifically for the 60+ demographic.

## Key Features

1. **Online Community**
   - Secure platform for users to connect, share stories, and support one another
   - Curated events, activities, and experiences tailored to seniors' interests and needs

2. **Holistic Support**
   - Expert advice and resources on health, wellness, finance, and legal matters
   - Partnerships with healthcare providers, hospitals, and labs for comprehensive medical services

3. **Learning and Growth**
   - Opportunities to learn new skills, explore hobbies, and engage in meaningful activities
   - Programs focused on digital literacy, language learning, and essential 21st-century skills

4. **Travel and Experiences**
   - Custom tour packages and unique travel experiences designed for seniors
   - Resources and tips for planning travel and outdoor activities

5. **Community Engagement**
   - Avenues for local and community meetups to foster connections among seniors
   - Opportunities for sharing personal stories and experiences

## Technology Stack

- **Backend**: Django
- **Frontend**: React and Angular
- **Database**: MySQL
- **Webmail**: Roundcube
- **Web Server**: Nginx
- **Containerization**: Docker Compose

## Hosting Environment

Gens.Life is hosted on OVH Worker 3, ensuring robust performance and scalability. The following services are deployed as Docker containers:

- **Database (MySQL)**: Port 3306
- **Django Backend**: Port 8000 (Gunicorn)
- **Nginx Web Server**: Ports 80 and 443
- **React Frontend**: Port 3000
- **PHP (for Roundcube Webmail)**: Port 9000
- **PhpMyAdmin**: Port 8080
- **Mail Server**: Various ports for SMTP, IMAP, and POP3
- **Roundcube Webmail**: Full-featured webmail client

### Static Site Management
- Static Site: Hosted on c3.supporthives.com

### Application Hosting
- React Application: app.gens.life (OVH Worker 3)
- Dynamic Django Site: api.gens.life (OVH Worker 3)

### Database Management
- MySQL database hosted on OVH Worker 3

## Domain Information

| Record Type | Name | TTL | Type | Value |
|-------------|------|-----|------|-------|
| SOA Record | gens.life | 3600 | SOA | buck.ns.cloudflare.com. dns.cloudflare.com. 2047832087 10000 2400 604800 3600 |
| NS Records | gens.life | 86400 | NS | buck.ns.cloudflare.com. |
|  | gens.life | 86400 | NS | isla.ns.cloudflare.com. |
| A Records | api.gens.life | 1 | A | 51.195.97.76 |
|  | app.gens.life | 1 | A | 51.195.97.76 |
|  | gens.life | 1 | A | 144.126.130.16 |
|  | mail.gens.life | 1 | A | 51.195.97.76 |
|  | webmail.gens.life | 1 | A | 51.195.97.76 |

*Note: For brevity, not all records are shown here. Please refer to the full documentation for complete domain information.*

## File Structure

```
/home/gens/
├── 16thSep_dbback.sql
├── 5thSep_dbbackup.sql
├── backup.py
├── docker-compose.yml
├── daily_backup.log
├── directory_structure.txt
├── django/
│   ├── docker-data/
│   ├── media/
│   └── roundcube/
├── django_backend/
│   ├── base/
│   ├── static/
│   └── ...
├── django_code/
│   ├── assets/
│   ├── authapp/
│   ├── coupon/
│   ├── documents/
│   └── ...
└── mysql_data/
    ├── #ib_16384_0.dblwr
    ├── ibdata1
    ├── mysql.sock
    └── ...
```

## Docker Compose Configuration

```yaml
version: '3.8'
services:
  django:
    build:
      context: ./django_code
    command: gunicorn GenS.wsgi:application --bind 0.0.0.0:8000
    volumes:
      - ./django_code:/code
    expose:
      - "8000"
  
  nginx:
    build:
      context: ./nginx_webserver
    volumes:
      - ./nginx_webserver/static:/app/static
      - ./nginx_webserver/media:/app/media
    ports:
      - "51.195.97.76:80:80"
      - "51.195.97.76:443:443"
    depends_on:
      - django
      - react
  
  react:
    build:
      context: ./react_frontend
    ports:
      - "51.195.97.76:3000:3000"
    volumes:
      - ./react_frontend:/app
```

## Getting Started

To set up the Gens.Life platform locally, follow these steps:

1. Clone the repository
2. Install Docker and Docker Compose
3. Run `docker-compose up --build`
4. Access the application at `http://localhost:3000`

For detailed setup instructions, please refer to our [Development Guide](link-to-dev-guide).

## Contributing

We welcome contributions to the Gens.Life platform! Please read our [Contributing Guidelines](link-to-contributing-guide) for more information on how to get started.

## License

This project is licensed under the [MIT License](link-to-license).

---

For more information, please visit our [official website](https://gens.life) or contact our support team at support@gens.life.
