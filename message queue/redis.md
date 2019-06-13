[Flask background job](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-xxii-background-jobs)

```shell
pip install rq
pip freeze > requirements.txt
```



[Redis Windows Download](<https://github.com/MicrosoftArchive/redis/releases>)

start redis server `redis-server`

Running the RQ Worker

```
(venv) $ rq worker microblog-tasks
18:55:06 RQ worker 'rq:worker:miguelsmac.90369' started, version 0.9.1
18:55:06 Cleaning registries for queue: microblog-tasks
18:55:06
18:55:06 *** Listening on microblog-tasks...
```



[Error 'module' object has no attribute 'fork' under Windows 10](<https://github.com/rq/rq/issues/859>)

[Windows Subsystem for Linux Installation Guide for Windows 10](<https://docs.microsoft.com/en-us/windows/wsl/install-win10>)

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```



[How to Install Python 3.7 on Ubuntu 18.04](<https://linuxize.com/post/how-to-install-python-3-7-on-ubuntu-18-04/>)

[Windows 上 Python 开发环境搭建](<http://www.zmonster.me/2016/09/10/use-python-on-windows.html>)

```
lynx -source rawgit.com/transcode-open/apt-cyg/master/apt-cyg > apt-cyg
install apt-cyg /bin

apt-cyg install wget vim gcc-core tmux sl

python -m ensurepip
python3 -m ensurepip
```

`cd /cygdrive/c`

`source activate`

`deactivate`