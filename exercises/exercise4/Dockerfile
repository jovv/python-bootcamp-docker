FROM python:3.8-slim

COPY . /code

RUN pip install -r /code/requirements.txt

EXPOSE 5000

ENTRYPOINT ["python"]

CMD ["code/app.py"]