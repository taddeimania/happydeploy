
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
9. Deploy to Heroku
 - git commit
10. Create custom User model in our `app/models.py`
 - `https://docs.djangoproject.com/en/2.0/topics/auth/customizing/#substituting-a-custom-user-model`
 - add `AUTH_USER_MODEL` attribute to `settings.py`
11. Add rest_framework and rest_framework.authtoken to `INSTALLED_APPS`
12. makemigrations & migrate
 - locally - `python manage.py migrate`
 - on heroku (git push (DEPLOY) all migrations and user model stuff first)
  - `heroku run python manage.py migrate`
13. Implement user login / logout (djoser)
 - `http://djoser.readthedocs.io/en/stable/authentication_backends.html#token-based-authentication`
 - Add djoser to `INSTALLED_APPS`
 - add paths to urls (you may need to import `include`)
 - run `python manage.py createsuperuser` to create superuser in app
 - Test user token creation works (run server).
  - POST to `/auth/token/create/` with Username and Password in request body
 - Test user token destroy works (Postman)
  - POST to `/auth/token/destroy/` with auth token as header (nothing in body): `Authorization: Token <paste token here>`
  - WOOPS!!!!! We didn't tell settings to use Token authentication for incoming requests:
  ```
  REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework.authentication.TokenAuthentication',
    )
  }
  ```
  - Now it should work.
14. Commit all changes and push to heroku
 - create superuser in Heroku
  - `heroku run python manage.py createsuperuser`
 - Test auth token create and destroy same as above - but with heroku host as URL
15. Add timestamp model to app
 - makemigrations and migrate locally
16. Heroku deploy (git add everything, commit, push)
17. Migrate new model on heroku
18. Create List and Create API View for Timestamp Model
 - create serializer for Timestamp model (serializers.py)
 - add queryset and serializer_class to API View
19. Add a path for timestamp api view
 - `path('timestamps/', TimestampListCreateAPIView.as_view())`
20. (Double check for any typos or import errors)
21. Test locally that you can GET to `/timestamps/` and POST to create a `/timestamps/`
