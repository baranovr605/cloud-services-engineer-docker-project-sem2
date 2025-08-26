FROM golang:1.21-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN go build -o app ./cmd/api

FROM alpine:3.22.1

EXPOSE 8081

WORKDIR /app

RUN apk add --no-cache curl

COPY --from=builder /app/app .

RUN addgroup --system appgroup && \
    adduser --system --ingroup appgroup appuser && \
    chown -R appuser:appgroup /app
USER appuser

CMD [ "./app" ]
