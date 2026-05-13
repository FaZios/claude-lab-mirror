# Ecosystem Master Plan — Fazio Lab → state-of-the-art maggio 2026

_Documento aggiornato 2026-05-12. Sezioni in ordine di lettura logico._

---

## 0. Cosa vuoi (in 3 frasi)

1. **Setup auto-mantenuto**: ogni modifica viene tracciata e allineata da sola, niente comandi da ricordare.
2. **Status sempre visibile**: in ogni momento sai cosa fa ogni progetto, dipendenze, stato deploy, prossimi step.
3. **Portabilità Claude Web ↔ Claude Code**: copi i file .md in Claude Web e lui sa subito a che punto sei.

Tutto questo con: **massima efficienza, minima manutenzione, contesto risparmiato, qualità invariata**.

---

## 1. Schema visivo — 3 stati

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                       │
│  IDEALE (cosa vuoi)              ATTUALE (cosa hai oggi)              │
│  ─────────────────               ──────────────────────               │
│                                                                       │
│  ┌─[Fazio]─────────┐             ┌─[Fazio]─────────┐                  │
│  │ "creo X"        │             │ "creo X"        │                  │
│  │ "dimmi status"  │             │ "dimmi status"  │                  │
│  │ "sync upstream" │             │ "sync upstream" │                  │
│  └────────┬────────┘             └────────┬────────┘                  │
│           │                                │                          │
│           ▼                                ▼                          │
│  ┌─[1 cmd → fatto]─┐             ┌─[manuale + ricordare]┐             │
│  │ /new <nome>     │             │ /new ✓ (NUOVO)       │             │
│  │ /status         │             │ /digest ✓            │             │
│  │ /sync           │             │ /sync ✓ ma manuale   │             │
│  └────────┬────────┘             │ status PER MANO ✗    │             │
│           │                      └────────┬────────────┘             │
│           ▼                               ▼                          │
│  ┌─[Sistema risponde]┐           ┌─[Sistema parziale]──┐             │
│  │ - Crea/aggiorna   │           │ - SessionStart hook  │             │
│  │ - Notifica TG     │           │ - Cron digest        │             │
│  │ - Aggiorna .md    │           │ - Auto status (3/30) │             │
│  │ - Commit+push     │           │ - Telegram alert ✓   │             │
│  │ - Memorizza KG    │           │ - KG mempalace ✓     │             │
│  └───────────────────┘           └──────────────────────┘             │
│                                                                       │
└─────────────────────────────────────────────────────────────────────┘

           SENIOR ENG GOOGLE/ANTHROPIC (best practice maggio 2026)
           ──────────────────────────────────────────────────────
           ┌─[Fazio]─────────────────────────────────────┐
           │ Qualsiasi prompt naturale                    │
           └───────────────┬─────────────────────────────┘
                           ▼
           ┌─[MCP server "fazio-projects"]───────────────┐
           │ get_state(X) │ list_active │ digest │ ...  │
           │ Anche Claude Web vede stesso state          │
           └───────┬─────────────────────────────┬───────┘
                   ▼                             ▼
           ┌─[Vector DB]─┐               ┌─[Auto-everything]┐
           │ Embedding   │               │ - CI/CD per proj │
           │ semantic    │               │ - Container dev  │
           │ search 30+  │               │ - Auto-doc       │
           │ progetti    │               │ - Auto-test gate │
           └─────────────┘               │ - Cost tracking  │
                                         │ - Auto-PR sync   │
                                         └──────────────────┘
```

---

## 2. Stato attuale (cosa hai già fatto, sommario)

### 2.1 Foundation (già pronta)
| Componente | Status | File |
|------------|--------|------|
| Modular architecture skill | ✓ | `~/.claude/skills/modular-architecture/` |
| Knowledge Graph cross-progetto | ✓ | mempalace MCP + `knowledge-graph.jsonl` |
| 30+ progetti con CLAUDE.md | ✓ | per-progetto |
| HARVEST findings auto | ✓ | `fazio-harvest` daemon |
| Cron weekly digest | ✓ | systemd timer Sun 09:00 |
| Telegram alerts | ✓ | hooks integration |
| Session tracking (crash recovery) | ✓ | session_tracker + finalizer |
| Cross-OS sync (Linux+Windows) | ✓ | link-claude-dirs.sh NTFS junction |
| 13 specialized agents | ✓ | `agents/` |
| 10 slash commands | ✓ | `commands/` |
| Sentrux Q gate | ✓ | hook pre-commit |
| Auto-scaffolder nuovi progetti | ✓ | `/new <name>` |
| Lineage detector upstream | ✓ | `lineage-detective` agent |
| Auto-archive stale files | ✓ | `stale_files_audit.py` |

### 2.2 Gap noti
| Gap | Impatto | Effort fix |
|-----|---------|------------|
| PROJECT_STATUS.md sez 4/6/7 manuali | medio | 1h (extend updater) |
| DASHBOARD.md presente solo in 3/30 progetti | basso | auto-genera mancanti |
| Modularity audit limitato a 5 progetti | medio | esegui per altri 25 |
| 2 duplicati files | minimo | ✓ FATTO ora |
| No MCP server custom "fazio-projects" | alto (Claude Web visibility) | 3-4h |
| No vector DB semantic search cross-prog | medio (context savings) | 1d |
| No CI/CD systematic per progetto | medio (quality) | 1 .yml per progetto |
| Test coverage non tracciato globalmente | medio | dashboard |
| 4 progetti richiedono refactor modularità | alto (upstream import) | 10gg dev |

---

## 3. Stato ideale (cosa vuoi raggiungere)

### 3.1 Esperienza utente target

| Scenario | Esperienza desiderata |
|----------|----------------------|
| Apro sessione qualsiasi progetto | Status fresh, upstream alert se pendenti, digest globale |
| Creo nuovo progetto | 1 comando crea tutto (struttura + repo + manifest + hooks) |
| Voglio sapere "a che punto è X" | Slash `/status X` → 1 markdown completo on-demand |
| Voglio info su X in Claude Web | Copio file .md → Web sa identità, stack, deploy, TODO |
| Upstream rilascia feature interessante | Telegram alert + agent propone integrazione testata |
| Tool nuovo scoperto da Harvest | Agent propone integration plan + decision A/B/C |
| Modifica file critico (es. fazio-core) | Auto-alert consumer impattati + suggerisce update |
| Crash sessione | Recovery automatico al next start, niente perso |
| Modifica codice in 1 progetto | Auto-update STATUS + auto-test + auto-commit |
| Voglio refactor cross-progetto | Agent `module-extractor` + `migrator` orchestrano |

### 3.2 Proprietà sistema

| Proprietà | Target |
|-----------|--------|
| **Comandi da ricordare** | 0 (tutto auto o suggerito proattivamente) |
| **File status manuali** | 0 sezioni dinamiche (manuali solo "Identity" + "Stack" stabile) |
| **Token wasted nel contesto** | <10% (lazy MCP load, on-demand) |
| **Drift detection** | Hook auto su modifica file critici |
| **Cross-project sync** | KG auto-update + alert downstream |
| **Time to status** | <5 sec per progetto qualsiasi |

---

## 4. State-of-the-art maggio 2026 (best practice senior eng)

Cosa farebbero ingegneri senior Google / Anthropic / Vercel per un setup come il tuo:

### 4.1 Core principles

1. **MCP-first** (Model Context Protocol Anthropic): tutti gli accessi a state via MCP server standardizzati. Claude Code + Claude Web + qualsiasi altro client parlano lo stesso linguaggio.
2. **Declarative config** (`.upstream-sources.toml` già fatto): stato dichiarato in TOML/YAML versionabili, non sparso in script.
3. **Event-driven hooks**: ogni azione genera eventi (SessionStart, PostToolUse, file change), hook reagiscono.
4. **Idempotency**: ogni script deve essere safe a re-run (fail-soft).
5. **Observability**: tracing + cost tracking per ogni session/agent/progetto.
6. **Self-healing**: detect drift + auto-fix dove sicuro, alert dove rischio.
7. **Versionato + lockfiles**: deps riproducibili (uv.lock, package-lock.json, Cargo.lock).
8. **Test gate prima di merge**: nessun commit senza test pass + Sentrux Q non scende.
9. **Container-based dev**: devcontainer.json per riproducibilità cross-OS.
10. **Auto-doc**: documentazione generata dal codice (FastAPI OpenAPI, typedoc, ecc.) — non scritta a mano.

### 4.2 Tool/algorithm specifici stato dell'arte 2026

| Categoria | Tool/algo | Use case Fazio |
|-----------|-----------|----------------|
| **AI coding agent** | Claude Code 1.x (Opus 4.7), Cursor, Codeium | già hai Claude Code |
| **MCP servers** | Anthropic stdlib, mempalace, github, filesystem | aggiungi custom fazio-projects |
| **Knowledge Graph** | mempalace, mem0, graphiti | mempalace già attivo |
| **Vector DB code search** | LanceDB, Chroma, Qdrant | aggiungi per 30 progetti |
| **Semantic search** | sentence-transformers (Qwen3-Embedding, mxbai) | per cross-project find |
| **CI/CD** | GitHub Actions, lefthook pre-commit | aggiungi systematic per-progetto |
| **Dependency mgmt** | renovate, dependabot, uv | adotta per auto-bump |
| **Test orchestration** | pytest, vitest, playwright, k6 | già usi pytest+vitest |
| **Quality gate** | Sentrux, SonarQube, Codecov | già hai Sentrux |
| **Container dev** | devcontainer.json, dagger, mise | mancante |
| **Doc auto-gen** | mintlify, fastapi.openapi, typedoc, rust-doc | mancante systematic |
| **Cost tracking** | ccusage, langfuse | ccusage già, langfuse in Atlas |
| **Telemetry** | OpenTelemetry, langfuse | Atlas già, espandi |
| **Code review AI** | code-reviewer agent + GitHub Copilot | hai entrambi |
| **Auto-PR generation** | gh CLI + agent | mancante |
| **Cross-project impact map** | mempalace + KG queries | parziale, da espandere |
| **Secrets management** | gh secret, BuildKit `--secret` | usi BuildKit |
| **Security scanning** | gitleaks, trufflehog, snyk | hai security-auditor agent |

### 4.3 Architettura raccomandata

```
┌──────────────────────────────────────────────────────────────────────┐
│                        FAZIO LAB ECOSYSTEM 2026                       │
├──────────────────────────────────────────────────────────────────────┤
│                                                                       │
│  CLIENT LAYER (interfaces)                                            │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐                │
│  │ Claude Code  │  │ Claude Web   │  │ Telegram     │                │
│  │ (CLI primary)│  │ (review/plan)│  │ (alerts/cmds)│                │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘                │
│         │                  │                 │                       │
│         └──────────────────┼─────────────────┘                       │
│                            │                                          │
│  MCP LAYER (standardized access)                                      │
│  ┌─────────────────────────────────────────────────────────────────┐ │
│  │ mempalace MCP │ fazio-projects MCP │ github MCP │ filesystem MCP│ │
│  │ KG cross-prog │ get_state/list/...  │ PR/issues  │ default       │ │
│  └─────────────────────────────────────────────────────────────────┘ │
│                            │                                          │
│  AGENT LAYER (specialized)                                            │
│  ┌─────────────────────────────────────────────────────────────────┐ │
│  │ 17 agents: researcher, orchestrator, upstream-syncer, dep-      │ │
│  │ bumper, harvest-porter, lineage-detective, code-reviewer,       │ │
│  │ artifact-verifier, test-gap-auditor, doc-writer, debugger, ...  │ │
│  └─────────────────────────────────────────────────────────────────┘ │
│                            │                                          │
│  AUTOMATION LAYER (hooks + cron)                                      │
│  ┌─────────────────────────────────────────────────────────────────┐ │
│  │ SessionStart: digest inject + status refresh + crash recovery    │ │
│  │ PostToolUse: live tracking, drift detect                         │ │
│  │ Stop: session finalize → PROJECT_STATUS.md update                │ │
│  │ Cron Sun 09:00: digest + stale audit + telegram alert            │ │
│  │ Pre-commit: Sentrux Q gate                                       │ │
│  └─────────────────────────────────────────────────────────────────┘ │
│                            │                                          │
│  DATA LAYER (declarative state)                                       │
│  ┌─────────────────────────────────────────────────────────────────┐ │
│  │ Per project: CLAUDE.md (manual), PROJECT_STATUS.md (manuale+auto)│ │
│  │   .upstream-sources.toml (manual+auto), DASHBOARD.md (auto)      │ │
│  │   HARVEST-FINDINGS.md (auto), .session-handoff.json (auto)       │ │
│  │ Global: _audit/IMPROVEMENTS-DIGEST.md, _audit/MODULARITY-AUDIT.md│ │
│  │   _audit/STALE-FILES-AUDIT.md, knowledge-graph.jsonl             │ │
│  │ Vector DB: embedding di tutto il codice (cross-project search)   │ │
│  └─────────────────────────────────────────────────────────────────┘ │
│                            │                                          │
│  EXECUTION LAYER                                                      │
│  ┌─────────────────────────────────────────────────────────────────┐ │
│  │ PC RTX 5080 (Linux) │ Book4 (Windows) │ Pi5 DietPi (deploy)     │ │
│  │ dev primary         │ mobile          │ 24/7 prod               │ │
│  └─────────────────────────────────────────────────────────────────┘ │
│                                                                       │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 5. Gap analysis (ideale vs attuale)

| Area | Gap | Priorità | Effort | Valore |
|------|-----|----------|--------|--------|
| **MCP server fazio-projects** | Manca. Claude Web non vede stato live | ALTA | 3-4h | ⭐⭐⭐⭐⭐ |
| **Vector DB semantic search cross-progetto** | Manca | MEDIA | 1d | ⭐⭐⭐⭐ |
| **PROJECT_STATUS sez 4/6/7 auto** | Manuale oggi | ALTA | 1-2h | ⭐⭐⭐⭐ |
| **CI/CD GitHub Actions per-progetto** | Solo Atlas + alcuni | MEDIA | 2h | ⭐⭐⭐ |
| **devcontainer.json per-progetto** | Manca | BASSA | 30min × prog | ⭐⭐ |
| **Auto-doc generation (OpenAPI, typedoc)** | Manuale | MEDIA | 1h × stack | ⭐⭐⭐ |
| **Cost tracking per progetto/sessione** | Solo aggregato ccusage | BASSA | 1h | ⭐⭐ |
| **Auto-PR generation per upstream sync** | Manuale via agent | MEDIA | 2h | ⭐⭐⭐ |
| **Modularity refactor 4 progetti** | Vedi MODULARITY-AUDIT.md | ALTA | 10gg | ⭐⭐⭐⭐⭐ |
| **Drift detection cross-OS** | Solo Linux check | MEDIA | 2h | ⭐⭐⭐ |
| **OpenTelemetry tracing agent calls** | Solo Atlas | BASSA | 1d | ⭐⭐ |
| **Renovate/dependabot per FaZios repo** | Manca | MEDIA | 1h | ⭐⭐⭐ |
| **Pre-commit lefthook globale** | Solo Atlas + alcuni | BASSA | 30min × prog | ⭐⭐ |

---

## 6. Roadmap prioritizzata

### Phase 1: Quick wins (oggi, ~6h)
| # | Azione | Effort | Cosa fa (in parole povere) |
|---|--------|--------|----------------------------|
| 1.1 | ✓ Consolida 2 duplicati | 5min | Niente file ridondanti |
| 1.2 | **MCP server `fazio-projects`** | 3-4h | Claude Code + Web + tutto vede stato uniforme. Niente più "leggi questo file" — chiedi al MCP |
| 1.3 | ✅ Extend PROJECT_STATUS auto-update (sez 4/6/7) — DONE 2026-05-13 | 1-2h | Status sempre fresco senza tocco manuale. T1 (sez 4/7) + T3 drift + T4 sentrux + T5 bridge ADR-0004 |
| 1.4 | Slash `/status [project]` per copy-paste Claude Web | 15min | 1 comando → markdown completo per Web |

### Phase 2: Strategic (settimana, ~10h)
| # | Azione | Effort | Cosa fa |
|---|--------|--------|---------|
| 2.1 | Vector DB indicizzazione 30 progetti | 1d | "Trova codice simile a X in tutti i progetti" — risparmio context enorme |
| 2.2 | CI/CD .yml per-progetto (template) | 2h | Test+lint auto su ogni push |
| 2.3 | Renovate config per FaZios org | 1h | Auto-PR dep bump |
| 2.4 | Refactor blocker job-ops (1-2gg) | 12-16h | Unlock 5 commit upstream pronti |
| 2.5 | ✅ Auto-PR generation upstream-syncer — DONE 2026-05-13 | 2h | Agent crea PR pronta da review. Body template enriched (T2): What was synced / Verification / Risks / Verdict sections |

### Phase 3: Long-term (mese, ~30h)
| # | Azione | Effort | Cosa fa |
|---|--------|--------|---------|
| 3.1 | Refactor altri 3 progetti modularità | 8gg | Atlas ✅ (2026-05-13, atlas_dashboard/ extract PR #3, -319 LoC); deal-sniper, trading-bot-farm pronti |
| 3.2 | devcontainer per-progetto | 30min × 30 | Riproducibilità totale dev env |
| 3.3 | OpenTelemetry tracing agent | 1gg | Sai dove vanno i tuoi token Claude |
| 3.4 | Auto-doc generation systematica | 4h | OpenAPI per FastAPI, typedoc per TS |
| 3.5 | Pre-commit lefthook tutti i progetti | 1gg | Format + lint + Sentrux gate |

---

## 7. Quick win immediato — MCP server `fazio-projects`

**Cosa è**: piccolo server Python che parla protocollo MCP (Anthropic standard). Espone funzioni "leggibili" a Claude:
- `list_projects()` → lista progetti attivi con health, stack, last commit
- `get_status(project)` → PROJECT_STATUS condensato (no need to read multiple file)
- `get_dashboard(project)` → DASHBOARD.md content
- `get_improvements()` → IMPROVEMENTS-DIGEST.md
- `get_lineage(project)` → upstream sources manifest
- `get_modularity_score(project)` → score from audit
- `get_open_todos(project)` → ## TODO section da CLAUDE.md
- `cross_project_impact(file)` → quali progetti dipendono da `file`

**Perché vale ⭐⭐⭐⭐⭐**:
- Claude Web può leggere stato live (oggi: nope, devi copy-paste file)
- Claude Code risparmia token (1 call MCP vs N read di file)
- Stessa fonte verità per qualsiasi client
- Funziona anche da Telegram bot futuro

**Cosa NON fa**: niente scrittura state — solo letture (separation of concerns, scrittura via hook esistenti).

**Effort**: 3-4 ore.

**Risparmio contesto stimato**: 50-70% per query "status progetto X" (oggi: 3-5 file letti = 5-10k token; con MCP: 1 chiamata = 500-1000 token).

---

## 8. Decisione richiesta

Procedo con **Phase 1** completa:
1. ✓ Consolidato duplicati (fatto sopra)
2. Costruisco MCP server `fazio-projects` (3-4h)
3. Estendo PROJECT_STATUS auto-update sez 4/6/7 (1-2h)
4. Aggiungo slash `/status` per copy-paste Web (15min)

Risultato: stato sempre fresco + Claude Web vede tutto + niente comandi da ricordare.

Conferma con OK o specifica un sub-step se preferisci.

---

## 9. Phase 2.6 + 2.7 — DEPLOYED 2026-05-12

### Phase 2.6 — Schema extension + 4 extractor scripts

Schema `.upstream-sources.toml` esteso con 4 sezioni auto-popolate:
- `[architecture]` — entry points, modules, LOC code/tests/docs, public funcs, API endpoints, modularity score
- `[deploy]` — host_address, container, image, port, healthcheck_url, health_status, uptime, last_check
- `[[tools]]` — adopted shared libs/services/MCP con upstream_repo, current_version, last_known_upstream, version_drift
- `[[consumers]]` — chi consuma il progetto, con relationship + via + match_count

Script `scripts/discovery/`:
- `architecture_extractor.py` — AST Python + grep Node/Rust, popola `[architecture]`
- `tools_version_checker.py` — GitHub API releases/latest vs installed (pip/npm/cargo), drift detection, Telegram alert
- `consumer_detector.py` — grep cross-progetto, popola `[[consumers]]`
- `deploy_state_checker.py` — SSH Pi5 + docker ps + compose parse, popola `[deploy]`

MCP server `scripts/mcp/fazio_projects_server.py` esteso con 4 nuovi tool:
- `fazio_get_architecture(project)`
- `fazio_get_tools_versions(project=None)` — aggregato cross-progetto se project omesso
- `fazio_get_consumers(project)`
- `fazio_get_deploy_state(project)`

Total tool count: 13 (era 9). Test gate `tools/list` passa, tutte le 4 nuove call restituiscono JSON valido.

`scripts/discovery/build_digest.py` extended con sezione "Tools version drift" + alert tracking via `.digest-state.json`.

`agents/harvest-porter.md` extended con Step 7b: registra adopted tool in `[[tools]]` quando consumers_count >= 2.

### Phase 2.7 — Retroactive rollout

`scripts/discovery/rollout_manifests.py` genera baseline manifest per progetti senza `.upstream-sources.toml`. Verdict auto-detect via git remotes (upstream → FORK; origin non-FaZios → FORK; default → ORIGINAL).

Risultati rollout:
- Progetti scansionati: 33
- Manifest pre-esistenti: 6 (Fazio-Atlas, job-ops, deal-sniper, llm-gateway, trading-bot-farm, exocortex)
- Manifest generati ex novo: 27 (di cui 26 committati, 1 SKIPPED — CUE ha merge conflict in altri file)
- Sezioni `[architecture]` popolate: 33/33
- Sezioni `[[consumers]]` popolate: 33/33 (con noise atteso per progetti con nome generico; refinement labels future)
- Sezioni `[deploy]` popolate: 33/33 (8 healthy, 25 not_deployed/unreachable)
- TOML parse check: 33/33 OK, 0 errori

### Status

| Componente | Stato |
|---|---|
| Schema template | DEPLOYED |
| 4 extractor scripts | DEPLOYED |
| 4 MCP tools | DEPLOYED |
| build_digest extension | DEPLOYED |
| harvest-porter workflow update | DEPLOYED |
| Rollout 27 progetti | DEPLOYED (26 commit landed, 1 deferred) |

---

_Fine master plan. Aggiornato 2026-05-12 con Phase 2.6 + 2.7 DEPLOYED._
