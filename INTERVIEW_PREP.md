INTERVIEW PREP — OpenTelemetry Demo
=================================

One‑line framing
----------------
"I deployed and validated a community OpenTelemetry microservice demo, exercised telemetry end‑to‑end, troubleshot runtime issues, and made a small config change to stabilize startup." Keep this sentence ready.

Top talking points (use 1–2 per answer)
- Project purpose: a realistic multi‑language microservice demo demonstrating distributed tracing, metrics, and logs.
- Deployment: supports local Docker Compose and generated Kubernetes manifests for cluster deployment.
- Observability flow: services export OTLP to the OpenTelemetry Collector; the collector exports to Jaeger (traces), Prometheus (metrics), and OpenSearch (logs).
- Instrumentation: service Dockerfiles and `genproto` scripts produce language bindings and include instrumentation agents or SDKs.
- Debugging: used Jaeger traces to find slow spans, Prometheus to identify resource pressure, and container logs/OpenSearch for root cause.
- Config changes: small, honest improvements (healthcheck timeout) demonstrate hands‑on capability.
- Testing: includes trace‑based tests and load generators to validate telemetry and system behavior.
- Learnings: container orchestration, telemetry pipelines, proto-driven APIs, and multi‑service debugging.

Likely questions & suggested one‑sentence answers
- How is telemetry routed? — "Services send OTLP to a local Collector which forwards to Jaeger, Prometheus, and OpenSearch for traces, metrics, and logs." 
- What did you actually change? — "I increased the OpenSearch healthcheck start_period/timeout to reduce false failures during startup; committed on branch `resume/demo-healthcheck`."
- How do you reproduce locally? — "Run `docker compose -f docker-compose.minimal.yml up --build -d`, trigger a request, then inspect Jaeger/Grafana/OpenSearch." 
- Where are service contracts? — "gRPC contracts are in `pb/demo.proto` and used by `genproto` scripts to generate clients." 
- How do you find a slow request? — "Open a trace in Jaeger, inspect slow spans, correlate with Prometheus metrics for CPU/memory, and check logs for errors." 
- How were Dockerfiles used? — "Each service under `src/*/Dockerfile` builds a container image and layers in instrumentation or language dependencies." 
- What would you add to improve this demo? — "Automated CI to run trace‑based tests and a reproducible smoke test that validates telemetry on each change." 
- How did you validate your change? — "Restarted the minimal compose stack, observed fewer healthcheck failures, and confirmed via `docker compose ps` and logs."

Honesty phrasing examples
- "I deployed and validated the demo, instrumented the run, and made small config changes — I didn't develop the application logic." 
- "I can show the commit and demonstrate the steps I took to verify telemetry flows and to stabilize startup." 

Quick demo checklist to mention
- `docker compose -f docker-compose.minimal.yml up --build -d`
- Jaeger: `http://localhost:16686` — view a trace
- Grafana: `http://localhost:55131` — open dashboard
- OpenSearch: `http://localhost:55125` — check logs/indices
