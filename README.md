Minimalist compose file for development of KoboToolbox

# Set up

1. Clone this repo in a new directory (maybe named kobo?)
2. Clone kpi and kobocat in the same directory `git clone git@github.com:kobotoolbox/kpi.git; git clone git@github.com:kobotoolbox/kobocat.git`
3. Edit environment variables as desired.
4. `docker compose up`
5. Migrate databases `docker compose run --rm kpi ./manage.py migrate` and `docker compose run --rm kobocat ./manage.py migrate` 

# Updates

1. Build on package changes `docker compose build --pull`
2. Migrate when new migrations are added  `docker compose run --rm kpi ./manage.py migrate` and `docker compose run --rm kobocat ./manage.py migrate` 

# Local kpi webpack dev server

1. Set env var `FRONTEND_DEV_MODE: host`
2. In kpi, run `npm i --force` and `npm run watch`
