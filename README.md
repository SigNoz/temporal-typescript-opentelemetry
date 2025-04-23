# Steps to run

1. Run a local temporal service or signup for a cloud account

Read about connecting to the account at https://docs.temporal.io/develop/typescript/temporal-clients

We use a very similar setup for connecting to temporal in this repo. Most of you would already have this connection implemented in your application.

We need to set envs to connect to your temporal namespace in the cloud account. Checkout `.env` file to replace values

2. Run `npm install` to install dependencies

3. Run the following command to start the worker
```
OTEL_EXPORTER_OTLP_ENDPOINT='https://ingest.<region>.signoz.cloud:443' OTEL_RESOURCE_ATTRIBUTES="service.name=temporal-worker-typescript,deployment.environment=test" OTEL_EXPORTER_OTLP_HEADERS="signoz-ingestion-key=<signoz-ingestion-key>" npm run start.watch
```

4. Run the following command to start the client
```
OTEL_EXPORTER_OTLP_ENDPOINT='https://ingest.<region>.signoz.cloud:443' OTEL_RESOURCE_ATTRIBUTES="service.name=temporal-client-typescript" OTEL_EXPORTER_OTLP_HEADERS="signoz-ingestion-key=<signoz-ingestion-key>" npm run workflow
```

You should start seeing sdk metrics, traces and logs appearing in signoz. For logging, the repo uses winston logger which is passed to temporal config and also sends data in otel format to SigNoz


# Notes
If you want to send the metrics and traces to your local otelcollector, use the below run commands:
For Worker
```
OTEL_EXPORTER_OTLP_ENDPOINT='http://localhost:4317' OTEL_RESOURCE_ATTRIBUTES="service.name=temporal-worker-typescript" npm run start.watch
```
For Client
```
OTEL_EXPORTER_OTLP_ENDPOINT='http://localhost:4317' OTEL_RESOURCE_ATTRIBUTES="service.name=temporal-client-typescript" npm run workflow
```


