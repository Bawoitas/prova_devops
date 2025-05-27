FROM python:3.11-alpine

WORKDIR /app

COPY app.py .

RUN pip install flask mysql-connector-python redis requests

EXPOSE 3002

CMD ["python", "app.py"]
