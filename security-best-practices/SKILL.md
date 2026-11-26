---
name: security-best-practices
description: Review or write secure-by-default application code when explicitly asked for security guidance, a security review, a report, or hardening. Supports Java 17+, .NET 8+, Python, JavaScript/TypeScript, and Go. Excludes general code review, debugging, and standalone threat modeling.
metadata:
  author: github.com/openai/skills
  version: '1.1.0'
---

# Security Best Practices

## Identify the stack and scope

Inspect runtime targets, dependency manifests, authentication schemes, deployment configuration and affected entry points. Include both frontend and backend in scope for a full-stack review. Apply version-specific advice to the version built and deployed by the project.

| Stack | Reference to load |
| --- | --- |
| Java 17+ | [Java backend](references/java-general-backend-security.md) |
| .NET 8+ | [.NET backend and ASP.NET Core](references/dotnet-general-backend-security.md) |
| Go | [Go backend](references/golang-general-backend-security.md) |
| Python | [Django](references/python-django-web-server-security.md), [FastAPI](references/python-fastapi-web-server-security.md), or [Flask](references/python-flask-web-server-security.md) |
| JavaScript/TypeScript server | [Express](references/javascript-express-web-server-security.md) or [Next.js](references/javascript-typescript-nextjs-web-server-security.md) |
| JavaScript/TypeScript browser | [General frontend](references/javascript-general-web-frontend-security.md) plus the applicable [React](references/javascript-typescript-react-web-frontend-security.md), [Vue](references/javascript-typescript-vue-web-frontend-security.md), or [jQuery](references/javascript-jquery-web-frontend-security.md) guide |

For other frameworks, verify the relevant version in primary documentation and disclose coverage gaps. Use the [CWE priorities and verification guide](references/cwe-priorities.md) for security review, hardening and control selection.

## Review and remediate

1. Trace external input and identity through entry points, authorization, data access, output and side effects. Check effective runtime settings, including ingress, proxies, deployment secrets and dependency versions when they affect the control.
2. Prioritize by reachability, prerequisites, impact and existing mitigations. Record the most specific verified CWE root cause. Distinguish confirmed issues from unverified configuration or deployment assumptions. Raise material security findings discovered during in-scope work.
3. For a review-only request, deliver findings. When remediation is requested, apply scoped fixes through existing framework controls and preserve legitimate behavior, supported runtime targets and existing data. Document authorized exceptions with their scope and compensating controls.
4. Verify the changed path through its normal entry point where possible. Check allowed behavior, rejection of invalid or unauthorized operations, and preservation of state on rejection. Run relevant builds and tests. For blocking I/O, new allocations, queries or shared state on a hot path, compare representative before/after throughput, latency and resource use against the project's budget. Iterate on observed failures or regressions and rerun impacted checks. Finish when checks pass or an external blocker prevents further validation. Record missing evidence.

For production TLS, verify termination and trust boundaries. Configure secure cookies for HTTPS deployments and evaluate HSTS against the site's HTTPS readiness. Enforce authorization even when public identifiers are opaque.

## Report

For a requested application audit, write to `security_best_practices_report.md` unless the user supplies a destination. Start with a short executive summary and scope. Order findings by severity and include a stable ID, concrete evidence with file and line, CWE, realistic impact, recommended mitigation, and verification status. Include test results, performance evidence where applicable, and residual risk. Summarize the key findings and link the report in the response.
