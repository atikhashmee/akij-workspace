# generic builder
FROM golang:alpine AS base

RUN apk add --no-cache git build-base

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN cp .env.example .env | true

#dev base builder
FROM base AS dev

RUN go install github.com/air-verse/air@latest

EXPOSE 3100

CMD ["air", "-c", ".air.toml"]

#generate apk
FROM base AS builder

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -ldflags="-s -w" -o goravel_app .

#production build
FROM alpine:latest AS prod

RUN apk add --no-cache ca-certificates tzdata

WORKDIR /var/www

COPY --from=builder /app/goravel_app .
COPY --from=builder /app/.env ./
COPY --from=builder /app/storage ./storage

EXPOSE 3100

ARG APP_USER=1000
RUN adduser -D -g '' $APP_USER
USER $APP_USER

CMD ["./goravel_app"]
