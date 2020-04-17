FROM ${imagepostpy}

RUN pip install flask pymongo

WORKDIR /app
ADD . /app

ENV ${POST_DATABASE_HOST}
ENV ${POST_DATABASE}

ENTRYPOINT ["python3", "post_app.py"]
