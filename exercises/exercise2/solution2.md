# Solution

Mount the `hello.py` file in the container and start it.
```cmd
cd exercises/exercise2
docker run -v %cd%/hello.py:/hello.py python:3.8-slim python hello.py
```