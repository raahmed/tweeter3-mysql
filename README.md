tweeter3
=======

Tweeter3 is a basic example Django application that uses [Django Rest Framework](https://github.com/encode/django-rest-framework)


## Installation Instructions

1. Clone the project.
    ```shell
    $ git clone https://github.com/nnja/tweeter3
    ```
2. `cd` intro the project directory
    ```shell
    $ cd tweeter3
    ```
3. Create a new virtual environment using Python 3.7 and activate it.
    ```shell
    $ python3 -m venv env
    $ source env/bin/activate
    ```
4. Install dependencies from requirements.txt:
    ```shell
    (env)$ pip install -r requirements.txt
    ```

5. Update static assets, make sure to run collect static.
```shell
(env) $ python manage.py collectstatic
```

### Set up your environment variables

See `.env-sample` for more details.

The following environment variables must be present in production:

```shell
# Configure the PostgreSQL Database
DB_USER="db_user"
DB_PASSWORD="db_password"
DB_NAME="db_name"
DB_HOST="db_host"
DB_PORT="db_port"

DJANGO_SETTINGS_MODULE="tweeter3.settings.production"
SECRET_KEY="my-secret-key"

# For deployment purposes, configure the Azure App Service Hostname
AZURE_APPSERVICE_HOSTNAME="myhost"

# Optionally, configure email error reporting by setting SEND_ADMIN_EMAILS="true"
# and configuring an email server and admin email addresses.
```

Configure them in a `.env` file, and then export the secrets:
```shell
$ set -a; source .env; set +a
```

## Create a certificate to enable SSL.

Follow Azure instructions on obtaining a certificate for connecting to MySQL servers over SSL.

### Create and configure an Azure MySQL Server and connect to it 

1. Navigate to the Azure Portal and search for MySQL server.

2. Create a server and configure Firewall settings.

3. Use the Azure MySQL tutorial to connect to your MySQL server. Once connected, create a MySQL database.

# Lastly, run migrations on your production database and optionally load fixtures.

```shell
# make sure all the production secrets are loaded in your current environment
set -a; source .env; set +a

# run production migrations
(env)$ python manage.py makemigrations
(env)$ python manage.py migrate

# Load fixtures, if desired.
(env)$ python manage.py loaddata initial_data
```

## Deploy to Azure App Service

Use ``` az webapp up -n <appname> ``` to deploy your service to Azure.
Then set the ApplicationSettings in your Azure Portal. In this, set your environment variables (as you did locally).
Restart the WebApp to see changes.


