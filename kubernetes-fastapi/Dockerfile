FROM tiangolo/uvicorn-gunicorn-fastapi:python3.8

RUN /usr/local/bin/python -m pip install --upgrade pip

RUN mkdir app

COPY requirements.txt /app/requirements.txt
RUN pip3 install --no-cache-dir -r /app/requirements.txt

RUN cd app

COPY ./service /app/service

EXPOSE 8080

RUN cd app
# Use the ping endpoint as a healthcheck,
# so Docker knows if the API is still running ok or needs to be restarted
WORKDIR /app

HEALTHCHECK --interval=21s --timeout=3s --start-period=10s CMD curl --fail http://localhost:8080/ping || exit 1
CMD ["uvicorn", "service.main:app", "--host", "0.0.0.0", "--port", "8080"]
