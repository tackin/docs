---
sidebar_position: 1
id: env-variables
title: Environment Variables
draft: true
---

| Variable                        | Description                                                            | Default Value                                        |
|---------------------------------|------------------------------------------------------------------------|------------------------------------------------------|
|**Basic Settings**  | | |    
| LOG_DRIVER                      | Defines the Docker Compose log driver used.                        | local                                               |
| INSECURE                        | Skips certificate validation for OpenCloud parts when using self-signed certificates. | true (should be commented out on internet-facing servers) |
|**Traefik Settings**  | | | 
| TRAEFIK_DASHBOARD               | Enables serving the Traefik dashboard.                             | false                                               |
| TRAEFIK_DOMAIN                  | Sets the domain for the Traefik dashboard.                         | traefik.opencloud.test                              |
| TRAEFIK_BASIC_AUTH_USERS        | Configures basic authentication for the Traefik dashboard.         | admin:admin (user "admin", password "admin")        |
| TRAEFIK_ACME_MAIL               | Specifies the email address for obtaining Let's Encrypt certificates. | None specified in source                           |
| TRAEFIK_ACME_CASERVER           | Used for testing the certificate process.                          | None specified in source                           |
|**OpenCloud Settings**  | | | 
| OPENCLOUD                       | Enables the core OpenCloud service.                                | :opencloud.yml                                      |
| OC_DOCKER_IMAGE                 | Defines the OpenCloud container image.                             | opencloudeu/opencloud-rolling                      |
| OC_DOCKER_TAG                   | Specifies the OpenCloud container version.                         | latest                                             |
| OC_DOMAIN                       | Sets the domain for the OpenCloud frontend.                        | cloud.opencloud.test                               |
| ADMIN_PASSWORD                  | Sets the OpenCloud admin user password.                            | admin                                              |
| DEMO_USERS                      | Determines whether demo users are created.                         | false                                              |
| LOG_LEVEL                       | Defines the OpenCloud log level.                                   | None specified in source                           |
| OC_CONFIG_DIR                   | Defines the OpenCloud configuration storage location.              | /your/local/opencloud/config (example path)        |
| OC_DATA_DIR                     | Defines the OpenCloud data storage location.                       | /your/local/opencloud/data (example path)         |
|**S3 Storage configuration - optional**  | | | 
| DECOMPOSEDS3                    | Enables S3 storage.                                                | :decomposeds3.yml                                  |
| DECOMPOSEDS3_ENDPOINT           | Configures the S3 storage endpoint.                                | http://minio:9000                                  |
| DECOMPOSEDS3_REGION             | Sets the S3 region.                                                | default                                            |
| DECOMPOSEDS3_ACCESS_KEY         | Specifies the S3 access key.                                       | opencloud                                          |
| DECOMPOSEDS3_SECRET_KEY         | Defines the S3 secret key.                                         | opencloud-secret-key                               |
| DECOMPOSEDS3_BUCKET             | Sets the S3 bucket.                                                | opencloud                                          |
| DECOMPOSEDS3_MINIO              | Adds local Minio S3 storage.                                       | :minio.yml                                         |
| MINIO_DOMAIN                    | Sets the Minio domain.                                             | minio.opencloud.test                               |
|**POSIX Storage configuration - optional**  | | | 
| POSIX                           | Enables POSIX storage.                                             | :posix.yml                                         |
|**SMPT settings**  | | | 
| SMTP_HOST                       | Specifies the SMTP host to connect to.                            | None specified in source                           |
| SMTP_PORT                       | Sets the port of the SMTP host.                                   | None specified in source                           |
| SMTP_SENDER                     | Defines the email address used for sending OpenCloud notification emails. | None specified in source                  |
| SMTP_USERNAME                   | Sets the username for the SMTP host.                              | None specified in source                           |
| SMTP_PASSWORD                   | Defines the password for the SMTP host.                           | None specified in source                           |
| SMTP_AUTHENTICATION             | Configures the authentication method for SMTP communication.      | None specified in source                           |
| SMTP_INSECURE                   | Allows insecure connections to the SMTP server.                   | false                                              |
|**Addititional services**  | | | 
| START_ADDITIONAL_SERVICES       | Defines additional services to start on OpenCloud startup.       | notifications                                      |
| EXTENSIONS                      | Enables the creation of a new named volume for web extensions.    | :web_extensions/extensions.yml                     |
| COMPANION_IMAGE                 | Specifies the Docker image for Uppy Companion.                   | None specified in source                           |
| COMPANION_DOMAIN                | Sets the domain for Uppy Companion.                              | companion.opencloud.test                           |
| COMPANION_ONEDRIVE_KEY          | Provider settings for OneDrive.                                  | None specified in source                           |
| COMPANION_ONEDRIVE_SECRET       | Provider settings for OneDrive.                                  | None specified in source                           |
| TIKA                            | Enables Tika (search).                                           | :tika.yml                                          |
| TIKA_IMAGE                      | Sets the desired Docker image tag or digest for Tika.            | latest                                             |
| COLLABORA                       | Enables Collabora web office.                                    | :collabora.yml                                     |
| COLLABORA_DOMAIN                | Sets the domain for Collabora.                                   | collabora.opencloud.test                           |
| WOPISERVER_DOMAIN               | Sets the domain for the wopiserver which handles OnlyOffice.     | wopiserver.opencloud.test                          |
| COLLABORA_ADMIN_USER            | Sets the admin user for Collabora.                               | admin                                              |
| COLLABORA_ADMIN_PASSWORD        | Sets the admin password for Collabora.                           | admin                                              |
| COLLABORA_SSL_ENABLE            | Enables SSL for Collabora Online.                               | false                                              |
| COLLABORA_SSL_VERIFICATION      | Enables SSL verification for Collabora Online.                  | false                                              |
| MONITORING                      | Enables monitoring.                                              | :monitoring_tracing/monitoring.yml                 |
| CLAMAV                          | Enables the ClamAV virus scanner.                               | :clamav.yml                                        |
| CLAMAV_DOCKER_TAG               | Sets the image version of the ClamAV container.                  | latest                                             |
| ONLYOFFICE                      | Enables OnlyOffice.                                              | :onlyoffice.yml                                    |
| ONLYOFFICE_DOMAIN               | Sets the domain for OnlyOffice [17].                                  | onlyoffice.opencloud.test                          |
| WOPISERVER_ONLYOFFICE_DOMAIN    | Sets the domain for the wopiserver which handles OnlyOffice [17].     | None specified in source                           |
| INBUCKET                        | Enables Inbucket, a mail catcher tool [17].                          | :inbucket.yml                                      |
| INBUCKET_DOMAIN                 | Sets the domain for Inbucket [18].                                    | mail.opencloud.test                                |
| COMPOSE_FILE                    | Assembles the supplemental compose files to be used [18].             | docker-compose.yml plus supplemental configs       |
