# When Agents Meet Physical Data: The Other Physics of Agent Harnesses

> Why coding agents fail on unstructured physical data (video, sensors, robot telemetry) and how a data harness with schemas, an execution engine, checkpoints, and a shared knowledge base fixes it.

- **Speaker:** Dmitry Petrov, DataChain
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=bUJgirn4_yc) (AI Engineer channel; ~28m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Petrov, who previously built DVC (data version control, "Git for data") and now works on DataChain, argues that agents need a data harness before they can work with physical data. He cites two frontier lab results from this year: Anthropic reported only 21 percent accuracy for its agents on data projects until specific data harnesses and context were added, and OpenAI described six layers of context needed to make a data agent work. Both of those, he notes, concern structured business data living in warehouses with tables and execution engines. His problem is harder: messy unstructured binaries in object storage, which he calls the extreme side of the data universe.

The core difficulty is what he calls an explosion of nested structure. A couple thousand video files look manageable on the surface, but recordings contain clips, clips contain frames, frames contain objects, and objects carry class, confidence, and bounding boxes. His metaphor is a neutron star: city-sized on the surface, heavier than the sun inside. In his demo, 90 dashcam videos generate roughly 100,000 detection records, and going deeper into objects multiplies that by 10 to 100. Teams typically respond by dumping metadata into millions of JSON files next to the images on S3 (bad latency, no consistency) or by standing up a centralized metadata database, which splits the stack into two systems and two languages that researchers avoid. Petrov's answer is Pydantic schemas as the single interface: data models, code, and queries all in Python, transpiled to SQL under the hood, with no SQL island in the codebase.

The demo shows DataChain's open source harness installed as a skill into Claude Code (three other coding agents are supported). The agent interviews the user about scope, picks a YOLO model at the smallest size, chooses per-frame granularity, and spends 24 minutes analyzing 91 January dashcam clips. Afterward, questions like "how many videos have people in them" run as fast local database queries (82 of 91 clips, in this case) instead of downloading and parsing JSON. The generated code is a plain Pydantic data model plus a filter, and file rows carry path, checksum, e-tag, and size from the cloud provider.

The rest of the talk covers the harness capabilities beyond seeing data. An execution engine connects Python functions, Pydantic input and output types, object storage, and the metadata warehouse, in what Petrov compares to Dask but for unstructured data; parallelism is a parameter, such as asking for 40 machines. Incremental updates and data checkpoints are a must-have because processing hundreds of thousands of files through LLM calls is expensive, and a mid-run failure should not force recomputing from scratch; reruns catch up on already-processed results and pick up only new files. For fast tests, the harness borrows dimensional modeling from the data warehouse tradition: when asked a question, the agent first asks itself whether a metadata layer exists that can answer it in a single SQL-ish query, and if not it builds one general enough to serve a family of related questions. Finally, datasets are shared through a knowledge base of markdown files recording description, session context, source code (which Petrov, citing OpenAI's data agent post, calls the most important part), schema, stats, and preview, so teammates' agents reuse computed slices instead of paying double or triple for the same compute. His closing point is that stronger models do not fix this; everyone already uses frontier models, and the harness is what changes the physics.

## Notable moments

- [0:00:30](https://www.youtube.com/watch?v=bUJgirn4_yc&t=30s) The framing stats: Anthropic's 21 percent accuracy on data projects without a harness, OpenAI's six layers of context.
- [0:08:10](https://www.youtube.com/watch?v=bUJgirn4_yc&t=490s) The demo run: 24 minutes to analyze 91 dashcam clips, then instant queries showing 82 clips contain people.
- [0:10:16](https://www.youtube.com/watch?v=bUJgirn4_yc&t=616s) The neutron star quantified: 90 videos become about 100,000 records, with object-level detail multiplying that by 10 to 100.
- [0:20:26](https://www.youtube.com/watch?v=bUJgirn4_yc&t=1226s) The agent asks itself whether it has the right metadata layer before answering, and builds a reusable one if not.

## Connections

- [Encord](../../companies/data-infrastructure/encord.md) sells the data layer for physical AI (robotics, AVs, drones), the same video-and-sensor territory Petrov's harness targets.
- [Deasy Labs](../../companies/memory-rag-search/deasy-labs.md) also bets that metadata over unstructured data is the bottleneck, though for enterprise documents rather than physical binaries.
- [ClickHouse](../../companies/data-infrastructure/clickhouse.md) is the warehouse-style analytics engine positioning for agents that Petrov says the unstructured world has to reinvent.
