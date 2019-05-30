# Celery

[Asynchronous Tasks in Python](<https://www.youtube.com/watch?v=fg-JfZBetpM&list=PLXmMXHVSvS-DvYrjHcZOg7262I9sGBLFR&index=1>)

[First Steps with Celery](<http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html>)

`pip install celery`

`celery worker -A tasks --loglevel=INFO --without-gossip --without-mingle --without-heartbeat -Ofair`

celery worker -A tasks --loglevel=INFO --pool=solo

