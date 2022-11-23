# Run django ORM query using jupyter notebook
### I am assuming django app in running in docker using docker compose services

## 1: Install Jupyter and django-extensions package
```commandline
docker compose exec <web-service-container-name> pip install django-extension jupyter
```

## 2: Expose notebook port in docker compose file in your web service
```dockerfile
ports:
    - "8000:8000"
    - "8888:8888"
```

## 3: Add notebook configuration in settings.py
```python
NOTEBOOK_ARGUMENTS = [
    '--ip', "0.0.0.0",
    '--port', '8888'
]
```

## 4: run server using extension
```commandline
docker compose exec <web-service-container-name> python manage.py shell_plus --notebook
```

## 5: Copy the url from terminal and open notebook in browser
create new shell_plus notebook from dropdown on top right corner of the jupyter notebook

## 6: Run the configuration to run our queries in asynchronous context
```python
import os
import django
os.environ.setdefault('DJANGO_SETTINGS_MODULE', '<root_app_name>.settings')
os.environ["DJANGO_ALLOW_ASYNC_UNSAFE"] = "true"
django.setup()
```
