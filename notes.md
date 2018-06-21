
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
