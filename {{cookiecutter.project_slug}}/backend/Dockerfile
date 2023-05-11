  
FROM python:3.10.11

WORKDIR /app

RUN apt update && \
    apt install -y postgresql-client && \
    apt clean

# Install pipenv and compilation dependencies
RUN pip install pipenv
RUN apt-get update && apt-get install -y --no-install-recommends gcc

# Applying pt_br language
RUN apt-get install -y locales locales-all
ENV LC_ALL pt_BR.UTF-8
ENV LANG pt_BR.UTF-8
ENV LANGUAGE pt_BR.UTF-8

COPY Pipfile .
COPY requirements.txt .
RUN pipenv install --deploy --ignore-pipfile -r requirements.txt

# Create and switch to a new user
RUN useradd --create-home appuser
WORKDIR /home/appuser
USER appuser

COPY . .
# Continue...