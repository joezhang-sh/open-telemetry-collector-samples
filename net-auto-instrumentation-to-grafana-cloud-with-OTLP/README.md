# Demo

## Description

This is a demonstrative example that uses Docker Compose.

It consists of following services:

1. [`client`](Client) - console application that makes a HTTP GET request
   instrumented with OpenTelemetry .NET Automatic Instrumentation.
2. [`service`](Service) - simple HTTP server using SQL Server.
   The application additionally has manual instrumentation (traces, metrics, logs)
   on top of the automatic instrumentation.
3. `otel-collector` - [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/)
   which collects the telemetry send by `client` and `service`
4. `grafana` - [Grafana](https://grafana.com/) as traces, metrics and logs backend

## Usage
Follow https://grafana.com/docs/grafana-cloud/send-data/otlp/send-data-otlp to get the token and update the 'Basic Auth' in 
exporters:
  otlphttp/grafanacloud:
    headers:
      Authorization: "{Basic Auth}"

Windows (Git Bash):

```sh
docker compose up -d --build
```

macOS and Linux:

```sh
make
```

You can [explore](https://grafana.com/docs/grafana-cloud/send-data/otlp/send-data-otlp/) to know how to send data to Grafana Cloud by OTLP

You can also find the exported telemetry in the `log` directory.

## Cleanup

Windows (Git Bash):

```sh
docker compose down --remove-orphans
rm -rf log
```

macOS and Linux:

```sh
make clean
```
