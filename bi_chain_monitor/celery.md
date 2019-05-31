# Celery

[[Youtube]Asynchronous Tasks in Python](<https://www.youtube.com/watch?v=fg-JfZBetpM&list=PLXmMXHVSvS-DvYrjHcZOg7262I9sGBLFR&index=1>)

[First Steps with Celery](<http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html>)

`pip install celery`

`celery worker -A tasks --loglevel=INFO --without-gossip --without-mingle --without-heartbeat -Ofair`

celery worker -A tasks --loglevel=INFO --pool=solo

tasks.py

```python
from celery import Celery
import time
app = Celery('tasks', backend='redis://localhost', broker='pyamqp://guest@localhost//')

@app.task
def add(a, b):
    print('add executing...')
    return a + b

@app.task
def sendmail(mail):
    print('Sending mail to {}'.format(mail['to']))
    time.sleep(2)
    print('Mail sent')
    return 'Send successful!'

@app.task
def reverse(string):
    return string[::-1]
```

client.py

```python
import time

from tasks import sendmail, add, reverse

print(sendmail.delay(dict(to='test@python.org')))

answer = sendmail.delay(dict(to='reply@python.org'))

while True:
    print("Waiting for ready")
    if answer.ready():
        break;
    time.sleep(0.5)

print(answer.get())

string = reverse.delay('hello')
print(string.get())
num = add.delay(3, 4)
print(num.get())
```

celery worker -A app.api.message_queue.test --loglevel=INFO --pool=solo

celery worker -A message_queue.tasks --loglevel=INFO --pool=solo

<http://docs.jinkan.org/docs/flask/patterns/celery.html>

```python
from celery import Celery

def make_celery(app):
    celery = Celery(app.import_name, broker=app.config['CELERY_BROKER_URL'])
    celery.conf.update(app.config)
    TaskBase = celery.Task
    class ContextTask(TaskBase):
        abstract = True
        def __call__(self, *args, **kwargs):
            with app.app_context():
                return TaskBase.__call__(self, *args, **kwargs)
    celery.Task = ContextTask
    return celery
```

任务在未来的某一时刻执行。例如，这个调用将安排任务运行在大约一分钟后:

```python
task = my_background_task.apply_async(args=[10, 20], countdown=60)
```

[在 Flask 中使用 Celery](http://www.pythondoc.com/flask-celery/first.html)

[flask celery 使用方法](https://www.cnblogs.com/huchong/p/9078661.html)

[使用 Celery 和 redis 完成任务队列](https://windard.com/opinion/2017/03/18/Task-Queue-Celery)

[Celery的最佳实践](<https://www.jianshu.com/p/cc3a0ffb9c76>)

[Celery 最佳实践](<http://einverne.github.io/post/2017/05/celery-best-practice.html>)

[python之celery使用详解一](https://www.cnblogs.com/cwp-bg/p/8759638.html)

[python之celery使用详解(二)](https://www.cnblogs.com/cwp-bg/p/10575688.html)

[celery 爬坑](<https://www.laoyuyu.me/2018/02/10/python_flask_celery/>)

