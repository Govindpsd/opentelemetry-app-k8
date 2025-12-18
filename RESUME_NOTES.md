RESUME NOTES
============

Quick summary
-------------
I deployed and validated a prebuilt OpenTelemetry microservice demo (Docker Compose + generated Kubernetes manifests). I focused on running the environment, validating telemetry flows (traces, metrics, logs), and making small, honest configuration improvements to demonstrate hands‑on work.

Concrete artifacts to reference
-------------------------------
- `docker-compose.yml` and `docker-compose.minimal.yml`
- `kubernetes/opentelemetry-demo.yaml`
- `pb/demo.proto`
- service Dockerfiles under `src/*/Dockerfile`
- observability configs: `src/jaeger/config.yml`, `src/grafana/grafana.ini`, `src/prometheus/prometheus-config.yaml`

Suggested resume bullets (honest, copy‑paste ready)
-------------------------------------------------
- Deployed and validated a 20+ microservice OpenTelemetry demo using Docker Compose and Kubernetes manifests to reproduce distributed tracing and metrics.
- Integrated and verified the observability stack (OpenTelemetry Collector, Jaeger, Prometheus, Grafana, OpenSearch) end‑to‑end across services.
- Used provided `genproto` scripts and service Dockerfiles to generate protobuf bindings and build container images for multi‑language services.
- Troubleshot runtime issues (healthchecks, GC pressure, startup order) using container logs, Jaeger traces, and Prometheus metrics.
- Created reproducible local runs via `docker-compose.minimal.yml` and documented verification steps for traces, metrics, and logs.
- Automated proto generation and validated trace‑based integration tests using the repo's test images.

Run & verify (minimal)
----------------------
1. Populate env or `.env` as needed.

```bash
docker compose -f docker-compose.minimal.yml up --build -d
```

2. Verify:
- Jaeger UI: http://localhost:16686
- Grafana: http://localhost:55131 (see dashboards)
- OpenSearch: http://localhost:55125 (check logs/indices)

Evidence / small hands‑on change
-------------------------------
If you want a direct commit to cite on your resume, create a branch `resume/demo-healthcheck`, add a small, honest change (for example, increase the `opensearch` healthcheck timeout in `docker-compose.yml`), and commit with message:

```
git checkout -b resume/demo-healthcheck
git commit -am "chore(demo): increase opensearch healthcheck timeout for more stable startup"
```

How to phrase this in interviews
--------------------------------
Be explicit and honest: "I deployed a community OpenTelemetry demo, validated telemetry end‑to‑end, troubleshot runtime issues, and made a small configuration change which I committed to demonstrate hands‑on ability." Emphasize what you learned (instrumentation flows, container resource tuning, cross‑service debugging).
