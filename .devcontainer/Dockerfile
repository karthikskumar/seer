FROM nvidia/cuda:12.1.1-cudnn8-devel-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive

ENV SOURCE_REPOSITORY=karthikskumar/jungle \
    POETRY_NO_INTERACTION=1 \
    POETRY_VIRTUALENVS_CREATE=false \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Prep apt
RUN apt-get update && apt-get install -y \
    python3 \
    python3-distutils \
    python3-pip \
    curl \
    git \
    # OpenCV Requirements
    ffmpeg \
    libsm6 \
    libxext6

# Install poetry
RUN curl -sSL https://install.python-poetry.org | python3 -
ENV PATH="/root/.local/bin:$PATH"

RUN curl https://raw.githubusercontent.com/${SOURCE_REPOSITORY}/main/pyproject.toml -O

# Install packages
RUN poetry add $(curl https://raw.githubusercontent.com/${SOURCE_REPOSITORY}/main/requirements.txt)

CMD echo "python --version" && echo "poetry --version" 
ENTRYPOINT /bin/bash