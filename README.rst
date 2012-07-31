"Abstract": The example code tests celery using rabbitmq.
The code was modified in order to support postgres, django-celery and django-pam.
Django-celery provides a basic interface for tasks monitoring and management.
Django-pam permits to login in django-admin using unix credentials.

This is a fork of the code of this tutorial_.
.. _tutorial: http://mathematism.com/2010/02/16/message-queues-django-and-celery-quick-start/

Please refer to the link above for the tutorial part.

**NOTE:** there's a typo in tutorial in the rabbitmq configuration part.
Use:
rabbitmqctl set_permissions -p myvhost myusername ".*" ".*" ".*"
instead of
rabbitmqctl set_permissions -p myvhost myusername "" ".*" ".*"

The code works in a python virtualenv with the following *dependencies*:
- Django==1.4
- amqplib==1.0.2
- anyjson==0.3.3
- celery==2.5.5
- django-celery==2.5.5
- django-pam==1.0
- django-picklefield==0.2.1
- importlib==1.0.2
- kombu==2.1.8
- ordereddict==1.1
- psycopg2==2.4.5
- python-dateutil==1.5
- virtualenv==1.5.1
- wsgiref==0.1.2

To start all the pieces in foreground open six terminal windows and type the following commands in each window:
- Window 1 *AMPQ broker*
  + ./sbin/rabbitmq-server
- Window 2 *Database*
  + ./bin/postgres -D ./pgsql/data
- Window 3 *Celery daemon*
  + python manage.py celeryd --verbosity=2 --loglevel=DEBUG -E
- Window 4 *Celery beat mode*
  + python manage.py celerybeat --verbosity=2 --loglevel=DEBUG
- Window 5 *Celerecam for task monitoring*
  + python manage.py celerycam
- Window 6 *Django dev server*
  + python manage.py runserver

