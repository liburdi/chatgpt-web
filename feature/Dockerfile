FROM golang:1.19

WORKDIR /app

COPY . /app/feature

WORKDIR /app/feature

RUN  make build

EXPOSE 8000

CMD ["sh", "-c", "/app/feature/bin/chatgpt-go"]