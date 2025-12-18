DEMO SCRIPT — 3 MINUTES
========================

Goal
----
Show a quick end-to-end run of the OpenTelemetry demo: start minimal services, generate sample traffic, and demonstrate a trace in Jaeger, a metric in Grafana, and a log in OpenSearch.

Timebox
-------
3 minutes total. Keep each section to ~45 seconds.

Preparation (30s)
- Ensure you are in the repo root and have required env vars or `.env` populated.

Commands to start minimal demo (30s)
-----------------------------------
Run the minimal set of services so startup is fast.

```bash
cd /path/to/opentelemetry-demo
docker compose -f docker-compose.minimal.yml up --build -d
```

Wait ~30–60s for services to be ready. You can watch lightweight logs:

```bash
docker compose -f docker-compose.minimal.yml logs --tail 50 --follow otel-collector jaeger grafana opensearch
```

Generate traffic (30s)
---------------------
Trigger a sample request that flows through the services and produces traces/metrics/logs. Example (adjust host/port as needed):

```bash
curl -sS http://localhost:8080/ | jq .  # or use the frontend/backends endpoints
# Or run the included load-generator for a few seconds if available
docker compose -f docker-compose.minimal.yml run --rm load-generator --duration 10s
```

Show a trace in Jaeger (45s)
---------------------------
- Open Jaeger UI: http://localhost:16686
- Select the service (e.g., `frontend` or `checkout`) and look for recent traces.
- Click one trace and narrate: root span (frontend HTTP), downstream gRPC calls, and any slow span found. Point out useful tags: `http.status_code`, span duration, and `trace-id`.

Show a metric in Grafana (30s)
-----------------------------
- Open Grafana: http://localhost:55131
- Load the Demo dashboard or search for the service CPU/memory or request latency panel.
- Highlight a spike or current value and explain how you correlate it with the trace shown in Jaeger.

Show a log in OpenSearch (30s)
-----------------------------
- Open OpenSearch / Kibana UI if available or query via curl:

```bash
curl -sS "http://localhost:55125/_cluster/health?pretty"
docker compose -f docker-compose.minimal.yml logs --tail 100 frontend | sed -n '1,50p'
```
- Point out a log line that corresponds to the request you traced (use trace-id if included in logs).

Wrap up (15s)
-------------
- Recap: started minimal demo, generated traffic, observed a trace in Jaeger, inspected a metric in Grafana, and found matching logs in OpenSearch.
- Offer to show additional details (proto contract at `pb/demo.proto`, service Dockerfiles under `src/*/Dockerfile`) or to reproduce a failing scenario.

Notes & troubleshooting
-----------------------
- If a service is slow to start, check `docker compose ps` and container logs. Increasing healthcheck timeouts can help for demo stability.
- Use `docker compose logs --tail 200 <service>` to collect evidence for post‑mortem.
