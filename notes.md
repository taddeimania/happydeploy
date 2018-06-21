
# End to End Django API in Heroku Notes

0. Install heroku-cli & do a heroku login

1. Make the virtual environment
 - .envrc
 - direnv allow
 - pip install pipenv
2. Install dependencies (that we know we will need)
 - Django
 - DRF
 - djoser
 - gunicorn
 - psycopg2-binary
 - django-heroku
3. Make the basic django app / project
 - django-admin startproject happydeploy .
3.1 Test application works
4. Start git repository
 - git init
 - add stuff to .gitignore
 - make initial commit
 - send code to github
4.1 Send code to github
 - create github repository
 - wire up local dir to remote repo
 - git push
5. Deploy to Heroku
 - heroku create
 - confirm w/ `git remote -v` - you should see origin & heroku
 - configure app to work in heroku
  - Add "\*" to ALLOWED_HOSTS (settings.py)
  - configure django_heroku
 - Add Procfile
  - Add web worker: `web: gunicorn happydeploy.wsgi`
 - Test app works locally
  - `heroku local web`
 - Commit all heroku stuff
 - Push code to Heroku to initiate deploy
  - `git push heroku master`
6. Start application
 - `python manage.py startapp <appname>`
7. Add Template View in `views.py`
 - Call it IndexView, configure class to use template
 - Create template directory in `app` dir
 - Create `index.html`
8. Wire up my view to the `/` route in `urls.py`
 - Test the route works in browser
 - When it doesn't work, make sure you've added your `app` to `INSTALLED_APPS`
