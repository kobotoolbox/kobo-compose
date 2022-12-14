# First run

Clone kpi and kobocat repos in this directory

1. Build `docker compose build --pull`
1. Migrate kobocat `docker compose run --rm kobocat ./manage.py migrate` (if the database didn't start yet, run `docker compose up` first)
1. Migrate kpi `docker compose run --rm kpi ./manage.py migrate`
1. Make user `docker compose run --rm kpi ./manage.py createsuperuser`
1. Edit `/etc/hosts` and add `172.17.0.1  kf.kobo.local kc.kobo.local ee.kobo.local`
1. Run `npm i --force` in the kpi directory.

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

# Rebuild docker images

If python packages in kpi or kobocat change, you can build like this

`docker compose build --pull`

Run migrate commands when new migrations are added

# Destroy everything and start over

Useful to remake databases.

1. `docker compose down`

Run first run steps again
