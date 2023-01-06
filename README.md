# asm-demos

This is a set of demo application set up to create signals and traces in Datadog ASM.

## Prerequisites

- Docker and Docker Compose.
- A Datadog API Key.

## Setup Process

For each one there is a `docker-compose.yml` file in their directory. This file can be used to start the application and the Datadog Agent. The Agent is configured to send traces and logs to Datadog.

Before launching the application copy `env.example` to `env` and fill in the API Key. This stays in the root of the repository, as it's used by each of the applications.

After setting up the env file, you can launch the application with:

```bash
docker compose up -d
```

Or if you've got the old version of Docker Compose:

```bash
docker-compose up -d
```

## DVWA

[DVWA](https://github.com/digininja/DVWA) is a PHP application that has a number of security issues you can trigger to see how Datadog ASM handles them.

After running the docker compose file, you can access it at http://localhost:5000. The default credentials are `admin:password`. The first time you access the application you'll need to set up the database. This can be done by clicking on the `Create / Reset Database` button at the bottom of the setup page. It will then push you back to the login page, where the same credentials will work.

### Example Vulnerability

Go to the SQL Injection item on the menu on the left and enter this into the ID box

```sql
 ' OR '1'='1
```

## NodeGoat

[NodeGoat](https://github.com/OWASP/NodeGoat) is another vulnerable application, this time written in Node.js. It has a number of security issues you can trigger to see how Datadog ASM handles them.

On first access you'll need to register a user. Any data can be used in the sign-up form, the e-mail address need to be in the form [user]@[domain].[TLD] but doesn't need to be a real valid e-mail address.

### Example Vulnerability

Go to the contributions page and enter this string into any of the form fields

```javascript
res.end(require('fs').readdirSync('.').toString())
```

## WebSite Tester

This is a test application which is useful for demonstrating SSRF vulnerabilities, written in Java.

After the Docker compose file has been run it can be accessed at http://localhost:8000/website.html

### Example Vulnerability

In the URL box on the page, put in a URL for an internal website which will return a response in your environment (e.g. `http://192.168.0.1`)