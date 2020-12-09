FROM python:3.8-slim
COPY ./api.py /app/api.py
COPY ./requirements.txt /app/requirements.txt

WORKDIR /app
RUN pip install -r requirements.txt

ENTRYPOINT ["python", "api.py"]