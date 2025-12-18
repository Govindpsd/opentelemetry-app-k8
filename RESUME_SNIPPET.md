Resume Snippet
==============

Project: OpenTelemetry Astronomy Shop (demo)

Summary (one line): Deployed and validated an OpenTelemetry multi‑service demo, exercised traces/metrics/logs, and stabilized local startup for reliable demos.

Key bullets (copy these into your resume under a project section):

- Deployed and validated a 20+ microservice OpenTelemetry demo using Docker Compose and Kubernetes manifests to reproduce distributed tracing and metrics.
- Integrated and validated observability: OpenTelemetry Collector, Jaeger (traces), Prometheus (metrics), Grafana (dashboards), and OpenSearch (logs).
- Generated protobuf bindings and built service images using provided `genproto` scripts and per‑service Dockerfiles for multi‑language clients.
- Troubleshot runtime issues (healthchecks, JVM GC pressure, startup order) using container logs, Jaeger traces, and Prometheus metrics; implemented targeted config changes to improve stability.
- Improved local demo reliability by tuning OpenSearch healthcheck timing and increasing container memory and JVM heap for stable startup.
- Automated reproducible local runs via `docker-compose.minimal.yml` and documented verification steps for traces, metrics, and logs.
