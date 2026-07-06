# Medic for Apache Spark: First Aid for Failing Jobs

> Pinterest's journey from a single ReAct prompt to a multi-agent Spark diagnostics system, with record-and-playback eval harnesses, an exception classifier, and metrics rendered as images to protect the context window.

- **Speaker:** Drasko Profirovic, Pinterest
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=0RNNfxpdbQk) (AI Engineer channel; ~12m; release date not captured in our metadata)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Profirovic, a staff engineer at Pinterest, built Medic to answer one question at scale: why did a Spark job fail? Data platform teams field a never-ending support rotation and have to ration attention between competing partner teams, while an LLM can scale that troubleshooting knowledge on demand. The vision was an agent that returns a deep research document with evidence for the root cause and suggested fixes grounded in the job's context, reachable from the surfaces users already work in, such as Slack and the Airflow UI.

The first version exposed Pinterest's data resources over MCP and leaned on careful human prompting, then graduated to a single ReAct agent with one prompt carrying the problem-solving approach, report structure, and example failure patterns. Beta trials exposed the limits. Prompt tuning became unsustainable because improving one area degraded another. Quality swung between shallow and verbose. Large log outputs consumed the context window and halted reasoning. Testing meant anecdotal manual runs against production data that would soon be retentioned away. The team responded with observability and testability: OpenTelemetry traces published to Langfuse to view executions as waterfalls, and an end-to-end harness with a record mode that captures real tool responses as fixtures checked in as code, plus a playback mode that runs analysis against fixtures and grades the report with offline evals. One example eval caps suggested fixes at three to control report verbosity. Profirovic says this let the team quantify quality instead of relying on intuition.

Two data-handling investments follow. For logs, regex filtering of benign exceptions did not scale, so they built an exception classifier pipeline that learns which exceptions commonly appear in successful jobs, treats those as likely red herrings, and filters them. The agent stopped reading logs directly and instead got two MCP tools, one returning the top-K truncated exceptions ranked by content relevance and recency relative to job termination, and one fetching full detail for a specific exception, which cut the chance of anchoring on a misleading stack trace. For metrics, raw time series are token-hostile for long production jobs, so a quarantined sub-agent converts them into annotated graphs collaged into a single image, similar to a Grafana dashboard with min and max callouts, and reasons about visual patterns such as executors dropping to zero or long plateaus. Images guarantee a fixed input token cost regardless of job duration, and only the summary returns to the parent agent.

The final architecture is multi-agent, built on LangGraph's deep agents library, with a dedicated prompt and MCP tool subset per agent plus built-in to-do list and virtual file system tools. Requests are classified as simple questions or deep diagnostics; a triage agent generates failure hypotheses, parallel research agents gather evidence and score root causes, a supervisor picks the highest-confidence one, and a healer agent proposes remediations from runbooks in a vector database. Profirovic notes they trialed LangGraph's deterministic workflows and found them brittle compared to ReAct. Next up: learning from user feedback across sessions and extending the pattern to Flink and Trino.

## Notable moments

- [0:02:05](https://www.youtube.com/watch?v=0RNNfxpdbQk&t=125s) The MCP-plus-single-ReAct-agent prototype and the shortcomings beta users surfaced.
- [0:04:06](https://www.youtube.com/watch?v=0RNNfxpdbQk&t=246s) Record and playback test harness: production tool responses become checked-in fixtures graded by offline evals.
- [0:06:07](https://www.youtube.com/watch?v=0RNNfxpdbQk&t=367s) The exception classifier that learns red-herring exceptions from successful jobs.
- [0:09:07](https://www.youtube.com/watch?v=0RNNfxpdbQk&t=547s) The multi-agent workflow: triage, parallel hypothesis research, supervisor selection, healer remediation.

## Connections

- [LangChain](../../companies/agent-orchestration/langchain.md): Medic's multi-agent rebuild is built on LangGraph's deep agents library, the runtime this profile covers.
- [Resolve.ai](../../companies/evals-observability/resolve-ai.md): the commercial analog, a multi-agent root-cause investigator for production incidents, where Medic is the in-house version for Spark.
