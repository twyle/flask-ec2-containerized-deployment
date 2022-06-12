# Flask Linode Deployment
> This is a simple flask application that shows how to deploy a production grade application to Linode.

[![Feature Development Build](https://github.com/twyle/flask-ec2-deployment/actions/workflows/feature-development-workflow.yml/badge.svg)](https://github.com/twyle/flask-ec2-deployment/actions/workflows/feature-development-workflow.yml)
[![Development Build](https://github.com/twyle/flask-ec2-deployment/actions/workflows/development-workflow.yml/badge.svg)](https://github.com/twyle/flask-ec2-deployment/actions/workflows/development-workflow.yml)
[![security: bandit][bandit-image]][bandit-url]
[![Imports: isort][isort-image]][isort-url]
[![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)](https://www.python.org/)
[![GitHub license](https://img.shields.io/github/license/Naereen/StrapDown.js.svg)](https://github.com/Naereen/StrapDown.js/blob/master/LICENSE)
![Medium](https://img.shields.io/badge/Medium-12100E?style=for-the-badge&logo=medium&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)
![Flask](https://img.shields.io/badge/flask-%23000.svg?style=for-the-badge&logo=flask&logoColor=white)
![Visual Studio Code](https://img.shields.io/badge/Visual%20Studio%20Code-0078d7.svg?style=for-the-badge&logo=visual-studio-code&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Gunicorn](https://img.shields.io/badge/gunicorn-%298729.svg?style=for-the-badge&logo=gunicorn&logoColor=white)

![](flask-linode.jpg)


This project shows how to lauch a production grade application to AWS EC2. It is a simple flask application, with the following features:
- ***A User Registration System.***
- ***A User Authentication and Authorization System.***
- ***A User Creation System.***
- ***Uses the PostgresQL Database to store both users as well as authentication and authorization information.***
- ***A logging system that logs to file and sends emails on critical errors.***
- ***It is deployed to an AWS EC2 instance with gunicorn server and nginx as a proxy.***

If you want to learn more about how it was developed, read ***[How to Deploy a Production Grade Flask application to a Linode Server Instance using GitHub Actions](https://medium.com/@lyle-okoth/how-to-deploy-a-production-grade-flask-application-to-an-aws-ec2-instance-using-github-actions-6241886b197)***. The are atleast five branches associated with the application:

- **Features** - Used to create new features
- **Development** - Where all the newly developed features are showcased
- **Staging** - Used to test out the nwely developed features before being moved to production
- **Release** - Holds all the code and assets related to the latest release
- **Production** - Holds all the code that is currentlyin production.

**The application development workflow. **

- A new feature branch is created, to host the code for the new feature.
- When this is pushed to GitHub, it triggers a workflow that does code quality checks as well as run unit tests, then tests that the application does run.
- When the feature branch is merged into the development branch, the same code quality checks are run. In addition , the code is pushed to the development server and then the application is restarted with the changes.
- The development branch is merged into the staging branch, following the same workflow, but the code is autodeployed to a staging server.
- When a tag is pushed to GitHub, the staging branch is merged into the Release branch and a release is created.
- When the rellease branch is merged into the production branch, the code is pushed to the production server and the production application restarted with the changes.

**The application routes.** 

The API has nine routes.

| Route       | Method      | Description      |
| ----------- | ----------- |----------------- |
| '/'         | GET         | Get the home page |
| '/user'     | GET         | Get a single user by supplying an ID |
| '/user'     | POST        | Create a new user by supplying the email address |
| '/user'     | PUT         | Update a single user's data by supplying the user ID and email address |
| '/user'     | DELETE      | Delete a single user by supplying the users ID |
| '/users'    | GET         | Get the list of all created users |
| '/auth/register'     | POST         | Register a new user. |
| '/auth/login'     | POST         | Login a registered user to get an access token. |
| '/auth/me'     | GET         | Get a logged in user's data. |

**The default (/) route :**

Simply returns a JSON response:

```json
{
  "hello": "from the template api!"
}
```

**The /users route :**

Simply returns a JSON response:

```json
[
  {
    "active": true, 
    "email": "test@example.com", 
    "id": 1
  }, 
  {
    "active": true, 
    "email": "test1@example.com", 
    "id": 2
  }
]
```
**The /user route :**

Simply returns the created, updated, deleted or requested user:

```json
{
    "active": true, 
    "email": "test@example.com", 
    "id": 1
 }
```

# Installation

### Clone the [Flask EC2 Deployment repo](https://github.com/twyle/flask-ec2-deployment)

```sh
git clone https://github.com/twyle/flask-ec2-deployment.git
```

### Navigate into the cloned repo

```sh
cd flask-ec2-deployment
```

### Create a Python3 Virtual Environment.

OS X & Linux:

```sh
python3 -m venv venv
```

### Activate the Virtual Environment.

OS X & Linux:

```sh
source venv/bin/activate
```

### Install the Project dependencies.

```sh
make update
make install
make install-dev
```

### Initialize pre-commit.

```sh
make pre-commit 
```

### Initialize pre-commit.

```sh
make initial-tag
```

### Create the PostgresQL database

Call it lyle_dev or whichever name you want

### Create the project secrets

```sh
touch .env
```
Then add the following to the file:

```sh
- FLASK_APP=api/__init__.py
- FLASK_ENV=development
- SECRET_KEY=supersecretkey

- POSTGRES_HOST=db 
- POSTGRES_DB=lyle
- POSTGRES_PORT=5432
- POSTGRES_USER=postgres
- POSTGRES_PASSWORD=lyle
```
### Create the database tables and seed data

```sh
make create_db
make seed_db
```

### Run the application
```sh
make run
```

### Test the application

```sh
make test-local
```

# Release History

## v0.3.0 (2022-06-02)

### Feat

- added the templates.

## v0.2.0 (2022-06-02)

### Feat

- implemented user data storage.

## v0.1.0 (2022-06-02)

### Feat

- created the authentication workflow.

## v0.0.1 (2022-06-02)

### Fix

- fixed the linting errors.
- fixed isort.

## Meta

Lyle Okoth – [@lylethedesigner](https://twitter.com/lylethedesigner) on twitter – [lyle okoth](https://medium.com/@lyle-okoth) on medium, and my email is lyceokoth@gmail.com

Distributed under the MIT license. See ``LICENSE`` for more information.

[https://github.com/twyle/github-link](https://github.com/twyle/)

## Contributing

1. Fork it https://github.com/twyle/flask-ec2-deployment/fork
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request

<!-- Markdown link & img dfn's -->
[wiki]: https://github.com/yourname/yourproject/wiki

[bandit-image]: https://img.shields.io/badge/security-bandit-yellow.svg
[bandit-url]: https://github.com/PyCQA/bandit

[isort-image]: https://img.shields.io/badge/%20imports-isort-%231674b1?style=flat&labelColor=ef8336
[isort-url]: https://pycqa.github.io/isort/

