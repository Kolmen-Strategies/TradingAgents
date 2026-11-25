# TradingAgents roadmap

Derived from README claims and source review on 2026-11-25 (`7c37249`). These are requirements or validation gaps, not active capabilities. Keep implemented scope and test status in [README.md](README.md). No delivery dates have been established.

| Priority | Advertised or implied capability | Evidence / gap | Completion criteria |
|---|---|---|---|
| P1 | Simulated exchange executes Portfolio Manager approvals | The former README claimed execution. `graph/trading_graph.py::_run_graph` logs and returns a rating; no simulated broker, order, fill or account ledger exists | Add a paper execution adapter, order/fill/position/cash accounting and integration tests that reconcile a complete round trip |
| P1 | Continuous portfolio risk management | Risk agents produce reports within one run; no portfolio feed, scheduling or execution-time limits | Add account/position inputs, measurable exposure/drawdown limits, monitoring and rejection tests |
| P2 | Social-post analysis and algorithmic sentiment scoring | `agents/analysts/social_media_analyst.py` only exposes `get_news`; `dataflows/interface.py` contains news vendors | Implement licensed social data collectors and explicit scored data with timestamp/provenance tests; retain the current news-based role meanwhile |
| P2 | Historical trading/backtesting fidelity | Date arguments exist, but financial statements/news APIs may expose current data and there is no broker-backed historical simulation | Point-in-time fixtures, look-ahead checks, an actual backtest/accounting harness and out-of-sample reports |
| P2 | Provider/model support proven in deployment | Factory supports ten providers; tests mostly validate local/mocked behavior. Bedrock was mentioned in setup but has no factory branch | Credential-gated smoke tests for each supported provider, structured-output fallback and error handling; implement Bedrock separately if that advertised enterprise option is retained |
| P2 | Docker/Ollama setup works end to end | Compose sets `LLM_PROVIDER`, which is not read by default config; loopback URLs in a container do not address the Ollama service | Wire provider/endpoint configuration, configure a pulled model, and validate CLI-to-Ollama operation inside compose |
| P2 | Recover a complete analysis after interruption | Existing checkpoint tests use a synthetic graph | Add full-graph fault injection with mocked tool/LLM calls; prove no duplicate decisions or unintended repeated external calls |
| P3 | Tested CLI, languages, data tools and automation | Unit tests pass, but live integrations/interactive UI/languages were not exercised; no checked-in CI workflow | Add CI for the current suite and deterministic full-pipeline tests, plus opt-in provider/data smoke checks |
| P3 | CLI invocation documentation | The installed single-command Typer app rejects a literal `analyze` subcommand; mocked CLI dispatch accepted bare `--checkpoint` | Keep examples matched to installed `--help` and CLI entry tests; avoid conflating mocked flag dispatch with a complete analysis |
| P3 | Accurate maintenance docs | `llm_clients/TODO.md` says validation is never called, but client warning/validation code and tests exist | Align secondary TODOs with the current client implementations; track remaining changes with source references |

Passing unit tests does not establish investment performance. The decision log's price-based outcome reflections do not constitute verified portfolio returns.
