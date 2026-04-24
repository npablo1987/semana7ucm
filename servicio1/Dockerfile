FROM  debian:12

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python3-venv \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt .

RUN python3 -m venv /opt/venv 

ENV PATH="/opt/venv/bin:$PATH"

RUN pip install --no-cache-dir -r requirements.txt

RUN django-admin startproject mi_proyecto .

RUN python manage.py migrate

EXPOSE 8000

CMD [ "gunicorn", "--bind", ":8000", "mi_proyecto.wsgi:application" ]