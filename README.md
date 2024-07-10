# First run

Clone kpi repo in this directory

1. Build `docker compose build --pull`
1. Start postgres `docker compose up postgres` this ensures it has time to initialize
1. Run Django database migrations `docker compose run -rm kpi scripts/migrate.sh`
1. Make user `docker compose run --rm kpi ./manage.py createsuperuser`
1. Edit `/etc/hosts` and add `127.0.0.1 kf.kobo.local ee.kobo.local`
1. Run `npm i` in the kpi directory.

# Start

1. `docker compose up`
1. Run frontend (in own tab) `cd kpi` and `npm run watch`

- KPI http://kf.kobo.local
- EE http://ee.kobo.local:8005 (or localhost:8005)

## Run with mailhog for graphical email testing

Mailhog will capture all emails sent, regardless of to address.

1. Start mailhog `docker compose -f docker-compose.mailhog.yml up`
2. Edit `docker-compose.yml` (or copy to `docker-compose.override.yml` to preserve original file) and uncomment `EMAIL_BACKEND: 'django.core.mail.backends.smtp.EmailBackend'`

Go to http://localhost:8025

## Python testing

1. Run from inside a container `docker compose exec -it kpi bash` (Assumes application is already running)
2. Install dev dependencies if not already done `pip install -r dependencies/pip/dev_requirements.txt`
3. Run Pytest  `pytest` or to run on a specific directory and reuse the DB (as a speedup) `pytest  --reuse-db kobo/apps/foo`.

# Rebuild docker images

If python packages in kpi or kobocat change, you can build like this

`docker compose build --pull`

Run migrate commands when new migrations are added

# Destroy everything and start over

Useful to remake databases.

1. `docker compose down`

Run first run steps again

## Text Editor lint, type checking, and type inference (Optional)

Many editors and cli tools can do type checking and type inference. However, it requires setting up a virtual environment.

1. Install Python 3 dependencies. For Ubuntu this is `apt install python3-dev python3-venv`
1. Create Python virtual environment `python3 -m venv env`
1. Activate environment `source env/bin/activate`
1. Install packages `pip install -r dependencies/pip/dev_requirements.txt`

These are not required but can improve the experience of editing code. Most text editors cannot read these dependencies from the docker container itself.
