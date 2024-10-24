ARG PULL_IMAGE
FROM ${PULL_IMAGE}-bullseye

RUN apt update && apt full-upgrade -y &&\
    apt -y install locales &&\
    apt autoremove && apt clean && apt autoclean &&\
    localedef -f UTF-8 -i ja_JP ja_JP.UTF-8;

ENV LANG ja_JP.UTF-8 \
    LANGUAGE ja_JP:ja \
    LC_ALL ja_JP.UTF-8 \
    TZ JST-9 \
    TERM xterm 

WORKDIR /workspace

# python env
ENV PYTHONUTF8=1 \
    PYTHONPATH="/workspace/python-app/src:$PYTHONPATH" \
    PYTHONPYCACHEPREFIX="/tmp/pycache" \
    POETRY_VERSION=${POETRY_VERSION} \
    POETRY_HOME=/opt/poetry \
    PYSETUP_PATH="/opt/pysetup" \
    PROJECT_PATH="./python-app"

# install poetry
RUN curl -sSL https://install.python-poetry.org | python && \
    cd /usr/local/bin && \
    ln -s /opt/poetry/bin/poetry && \
    poetry config virtualenvs.create false

# dev Tools
RUN apt-get install -y vim less
RUN echo "alias ll='ls -la --color'" >> /root/.bashrc

# install package
WORKDIR $PYSETUP_PATH
# COPY ["${PROJECT_PATH}/pyproject.toml", "${PROJECT_PATH}/poetry.lock", "./"]
# RUN poetry install
