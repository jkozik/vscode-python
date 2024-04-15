# [Setting A Dockerized Python Environment — The Hard Way](https://medium.com/towards-data-science/setting-a-dockerized-python-environment-the-hard-way-e62531bca7a0)
This article by [Rami Krispin](https://medium.com/@rami.krispin) outlines the basic steps for setting up a python environment in docker.  

## build image
```
jkozik@u2004:~/projects/vscode-python$ docker build . -t my_python_env:3.10  
[+] Building 41.7s (10/10) FINISHED                                                docker:default
 => [internal] load build definition from Dockerfile                                         0.0s
 => => transferring dockerfile: 350B                                                         0.0s
 => [internal] load metadata for docker.io/library/python:3.10                               0.0s
 => [internal] load .dockerignore                                                            0.0s
 => => transferring context: 2B                                                              0.0s
 => [1/5] FROM docker.io/library/python:3.10                                                 0.2s
 => [internal] load build context                                                            0.1s
 => => transferring context: 396B                                                            0.0s
 => [2/5] RUN mkdir requirements                                                             0.4s
 => [3/5] COPY requirements.txt set_python_env.sh /requirements/                             0.1s
 => [4/5] RUN bash ./requirements/set_python_env.sh my_env                                  24.2s
 => [5/5] RUN apt-get update &&     apt-get install -y     vim     && apt update            12.7s
 => exporting to image                                                                       3.9s
 => => exporting layers                                                                      3.9s
 => => writing image sha256:a075db548f78851e3be72aedabccdda3f6c6d60e9badbc5a2be0eeb9679cc93  0.0s
 => => naming to docker.io/library/my_python_env:3.10                                        0.0s
jkozik@u2004:~/projects/vscode-python$
```

## Verify basic python
```
(my_env) root@7693e984d446:/# python
Python 3.10.14 (main, Apr 10 2024, 15:10:24) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 1+1
2
>>> 
```

## Verify volume mount

jkozik@u2004:~/projects/vscode-python$ docker run -it -v .:/my_scripts my_python_env:3.10
(my_env) root@316a9a10e9ec:/# ls my_scripts/
Dockerfile  requirements.txt  set_python_env.sh
(my_env) root@316a9a10e9ec:/# ls my_scripts/
```