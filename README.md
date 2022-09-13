# First run

1. Build `docker compose build --pull`
1. Migrate kobocat `docker compose run --rm kobocat ./manage.py migrate`
1. Migrate kpi `docker compose run --rm kpi ./manage.py migrate`
1. Make user `docker compose run --rm kpi ./manage.py createsuperuser`
1. Edit `/etc/hosts` and add `172.17.0.1  kf.kobo.local kc.kobo.local ee.kobo.local`

If running webpack locally run `docker compose run --rm kpi npm run build`

# Start

1. `docker compose up`
1. Run frontend (in own tab) `cd kpi` and `npm run watch`

- KPI http://kf.kobo.local
- EE http://ee.kobo.local:8005 (or localhost:8005)

# Rebuild docker images

If python packages in kpi or kobocat change, you can build like this

`docker compose build --pull`

Run migrate commands when new migrations are added

# Destroy everything and start over

Useful to remake databases.

1. `docker compose down`

Run first run steps again
