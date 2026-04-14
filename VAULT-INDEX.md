# Vault Dashboard

## Current Priorities
- Start capturing real work knowledge into the vault
- Connect SharePoint for work document access

## Active Projects

### webcaller
Twilio-based call testing platform for ServiceNow voice agents. Frontend (Netlify), backend toolkit (EAI), sync pipeline.
- **voicecoval4** — Primary instance. Sync reliability, transcript cleaning, eval app pipeline
- **emppupadhyaya** — Second SN instance (Genesys Cloud subtype, multi-instance sync)
- **softphone** — New feature: custom number calling with recording (spec written, pending impl)

### Other projects
- [[01_projects/investigate-call-skill]] - Claude Code skill for debugging PAVA voice agent calls
- snc-pava - OTel tracing, TTS fix (inferno `tts_content`), debug flow PR #1094, Spec Kit eval, per-service CLAUDE.md
- coval - Voice agent regression testing: test set management, v2v architecture comparison, coval_agent.py wrapper, resimulator
- voice-workbench - Reproducible audio injection test framework for PAVA (design phase)

## Recent Decisions
- Obsidian + QMD + Claude Code stack for work second brain (2026-04-06)
- Global skills over project-specific commands (2026-04-06)
- CLAUDE.md behavior over custom slash commands for simplicity (2026-04-06)
- Consolidated webcaller subprojects under single umbrella project (2026-04-13)

## Open Threads

### Webcaller
- [x] ~~Deploy backend toolkit with subtype_filter change so emppupadhyaya records sync automatically~~ — deployed, both instances syncing (2026-04-13)
- [x] ~~IMS0019172 not yet in processed_records.csv~~ — emppupadhyaya sync running, record processed (2026-04-13)
- [x] ~~voicecoval4 TwiML endpoint updated with dynamic hostname~~ — committed and deployed (2026-04-13)
- [x] ~~Race condition fix (96fa337) + audio swap fix (b7afde0)~~ — deployed, no errors in logs (2026-04-13)
- [ ] Monitor catchup sweep effectiveness — confirm it catches late-arriving records within 10-min interval (2026-04-09)
- [ ] Job stability: sync job crashes mid-cycle — uninvestigated (2026-04-08)
- [ ] Test call for emppupadhyaya — hasn't worked end-to-end yet, investigate call flow (2026-04-13)
- [ ] Review softphone spec (`webcaller/softphone_spec.md`) and create TwiML App before implementation (2026-04-10)
- [ ] Verify `+16413396567` is a valid Twilio caller ID for softphone (2026-04-10)
- [ ] Test browser → backend access — sync.js suggests it may work, could simplify softphone architecture (2026-04-10)
- [ ] Consider removing `docker compose push` Makefile target in favor of direct `docker push` (2026-04-10)

### snc-pava
- [x] ~~PAVA TTS: PR needed in Cartesia/inferno agent to read `tts_content`~~ — resolved (2026-04-13)
- [ ] OTel tracing: implement hybrid approach in orchestrator (OTel spans → DebugFlowSpanProcessor + OTLP export), check K8s for Tempo (2026-04-10)
- [ ] PR #1094 (debug flow): status uncertain — implementation approach depends on whether it merges (2026-04-10)
- [ ] Evaluate Spec Kit (github/spec-kit) for PAVA team collaboration — trial setup on branch (2026-04-10)
- [ ] Resolve CLAUDE.md merge strategy — Spec Kit wants to manage CLAUDE.md, need coexistence plan (2026-04-10)
- [ ] Fill in missing per-service CLAUDE.md files: common/, stt_server/, glide_mock/ (2026-04-10)
- [ ] Share surfseuat OOB catalog agent timeout findings with other team — fix options: increase timeout, trim tool descriptions, avoid JSON regurgitation (2026-04-08)
- [ ] Voice-vs-chat endpoint difference (TEXTCHAT→WEBRTC header) — could Glide return different agent/tool configs based on source header? (2026-04-08)

### Coval
- [x] ~~Check v2v run results (`Knx35XzWpsskYaQuoKwnwt`) — launched Apr 8~~ — resolved (2026-04-13)
- [x] ~~Clarify "create incident" test case request — which agent/flow?~~ — resolved (2026-04-13)
- [x] ~~Coval CLI em dash bug — file PR on `coval-ai/cli` (needs write access / fork)~~ — resolved (2026-04-13)
- [x] ~~Kill old `coval_resimulator` job once `resimulator` is confirmed stable~~ — resolved (2026-04-13)
- [x] ~~Verify resimulator named URL works after port fix~~ — resolved (2026-04-13)

### Voice Workbench
- [ ] Design multi-turn completion signaling protocol (2026-04-10)
- [ ] Plan barge-in / interruption test support (2026-04-10)
- [ ] Define latency capture and assertion per turn (2026-04-10)
- [ ] Decide on audio sourcing strategy: real recordings vs synthesized (2026-04-10)
- [ ] Build regression tracking — store results with build identifiers for CI trends (2026-04-10)

### Investigate-call skill
- [ ] Test full investigation flow end-to-end to confirm wrappers eliminate all permission prompts (2026-04-08)

### Vault / Tooling
- [ ] Connect SharePoint via Composio for work document access
- [ ] Decide on folder structure for projects as they come in
- [ ] Schedule `/consolidate` after vault has enough content
- [ ] Install Dataview plugin in Obsidian and test queries
- [ ] Consider auto-archive logic for CLAUDE.md and mistakes-and-lessons.md when they get large (2026-04-06)

## Knowledge Base
- [[02_knowledge/voice-agent-data-sources]] - Splunk vs sys_generative_ai_log vs interaction transcript: when to use each
- [[02_knowledge/architecture/pava-observability-state]] - PAVA metrics, tracing, OTel current state + planned hybrid approach

## Quick Links
- [[CLAUDE.md]] - Operating instructions
- [[mistakes-and-lessons]] - Error log
