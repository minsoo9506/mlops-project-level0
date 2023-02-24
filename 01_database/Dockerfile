FROM amd64/python:3.9-slim

RUN apt-get update && apt-get install -y \
    postgresql-client \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/app

RUN pip install -U pip &&\
    pip install scikit-learn pandas psycopg2-binary

COPY 03_data_generator_in_docker.py 03_data_generator_in_docker.py

ENTRYPOINT [ "python", "03_data_generator_in_docker.py", "--db-host" ]

CMD ["localhost"]