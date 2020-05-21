FROM python:3.6.0-alpine
WORKDIR /app
ADD requirements.txt /app
RUN pip install -r requirements.txt
ENV POST_DATABASE_HOST=post_db
ENV POST_DATABASE=posts
ADD . /app
EXPOSE  5000
ENTRYPOINT ["python3", "post_app.py"]
