#  Licensed to the Apache Software Foundation (ASF) under one   *
#  or more contributor license agreements.  See the NOTICE file *
#  distributed with this work for additional information        *
#  regarding copyright ownership.  The ASF licenses this file   *
#  to you under the Apache License, Version 2.0 (the            *
#  "License"); you may not use this file except in compliance   *
#  with the License.  You may obtain a copy of the License at   *
#                                                               *
#    http://www.apache.org/licenses/LICENSE-2.0                 *
#                                                               *
#  Unless required by applicable law or agreed to in writing,   *
#  software distributed under the License is distributed on an  *
#  "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY       *
#  KIND, either express or implied.  See the License for the    *
#  specific language governing permissions and limitations      *
#  under the License.                                           *

FROM alpine:3.7

COPY airflow.tar.gz /tmp/airflow.tar.gz
COPY bootstrap.sh /bootstrap.sh

RUN apk add --no-cache --virtual build-deps \
        python3-dev \
        libressl-dev \
        libffi-dev \
        build-base \
        postgresql-dev \
        libxml2-dev \
        libxslt-dev \
        linux-headers && \
    apk add --no-cache \
        bash \
        py3-requests \
        curl \
        rsync \
	wget \
        netcat-openbsd && \
    adduser -D -s /bin/bash -h /home/airflow/ airflow && \
    pip3 install -U pip && \
    pip3 install -U setuptools && \
    pip3 install kubernetes && \
    pip3 install cryptography && \
    pip3 install psycopg2 && \
    pip3 install /tmp/airflow.tar.gz && \
    apk del --no-cache build-deps && \
    apk add --no-cache libpq && \
    rm -f /tmp/* && \
    chmod +x /bootstrap.sh

USER airflow

ENTRYPOINT ["/bootstrap.sh"]
