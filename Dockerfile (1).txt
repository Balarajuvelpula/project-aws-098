FROM python:3.10

WORKDIR /app

# system dependencies install
RUN apt-get update && apt-get install -y \
    openssl \
    libssl-dev \
    gcc

# copy project files
COPY . /app

# python dependencies
RUN pip install --no-cache-dir pyOpenSSL cryptography flask

# expose port
EXPOSE 5000

# run application
CMD ["python", "main.py"]
