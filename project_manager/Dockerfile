
FROM node:16-alpine AS builder

WORKDIR /frontend

COPY ./frontend .
RUN npm install
RUN npm run build
# ============================================================

FROM python:3.10

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV DOCKERIZE_VERSION v0.2.0  

WORKDIR /code
COPY requirements.txt ./
COPY base_model_data.json ./
RUN pip install -r requirements.txt

RUN apt-get update
RUN apt-get -y install libgl1-mesa-glx

RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \  
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

COPY . .

COPY --from=builder /frontend /frontend