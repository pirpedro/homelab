FROM arm64v8/golang AS builder

RUN apt update && apt install git ca-certificates mailcap -y

WORKDIR /app

RUN curl --remote-name-all https://raw.githubusercontent.com/KostyaEsmukov/smtp_to_telegram/master/{go.sum,go.mod,smtp_to_telegram.go,smtp_to_telegram_test.go}

ENV GOARCH=arm
ARG ST_VERSION=0.1
ARG GOPROXY=direct
RUN CGO_ENABLED=0 GOOS=linux go build \
        -ldflags "-s -w \
            -X main.Version=${ST_VERSION:-UNKNOWN_RELEASE}" \
        -a -o smtp_to_telegram

FROM arm64v8/alpine:3.19

RUN apk add --no-cache ca-certificates mailcap

COPY --from=builder /app/smtp_to_telegram /smtp_to_telegram

USER daemon

ENV ST_SMTP_LISTEN="0.0.0.0:2525"
EXPOSE 2525

ENTRYPOINT ["/smtp_to_telegram"]
