FROM ubuntu:22.04
RUN apt-get update && apt-get install \
    pip \
    libldap2-dev \
    libsasl2-dev \
    libmysqlclient-dev \
    -y 
RUN pip install mysql-connector-python
RUN mkdir /etc/privacyidea
RUN useradd -r privacyidea
COPY ./src/privacyIDEA-3.11.1.tar.gz /src/
RUN pip install /src/privacyIDEA-3.11.1.tar.gz 
CMD ["pi-manage", "run", "--host", "0.0.0.0"]
