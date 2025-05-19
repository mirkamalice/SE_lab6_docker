<h1>گزارش آزمایش 6</h1>

کار با داکر

------------------------------------

فایل 

Dockerfile:

```
# Dockerfile
FROM python:3.11

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

```

فایل 

docker-compose.yml:

```
version: "3.9"

services:
  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    ports:
      - "8000:8000"
    env_file:
      - .env
    depends_on:
      - db
    volumes:
      - .:/app

  db:
    image: postgres:15
    volumes:
      - postgres_data:/var/lib/postgresql/data/
    environment:
      POSTGRES_DB: test
      POSTGRES_USER: user1
      POSTGRES_PASSWORD: 123456

volumes:
  postgres_data:

```

فایل 

requirements.txt