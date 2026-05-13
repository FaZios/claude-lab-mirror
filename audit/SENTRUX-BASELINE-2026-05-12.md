# Sentrux Baseline — 2026-05-12 (post-M3 consolidation)

**Run**: 2026-05-12 fresh rescan (Linux build available — TIER-A 7/7 refreshed)
**Method**: `sentrux gate --save` per TIER-A repo via Linux binary v0.5.7.
**Status**: Linux build resolved. Binary `~/.local/bin/sentrux` (downloaded from upstream releases, NOT custom-built). TIER-A 7/7 baselines refreshed.
**Source**: `sentrux/sentrux` upstream provides pre-built `sentrux-linux-x86_64` (36MB ELF, dyn-linked GNU/Linux 3.2+, 51 tree-sitter grammars auto-fetched). Cargo build skipped — release binary fits exact use case.

## Scope

- Projects scanned: **31**
- TIER-A active: 6/7 (browser-pool MISSING — never scanned, new project)

## Full ranking (Q score desc)

| # | Project | Q | Coupling | Cycles | God | Hotspots | Complex fns | Edges | Cross | Date | Age (d) | TIER-A |
|---|---------|---|----------|--------|-----|----------|-------------|-------|-------|------|---------|--------|
| 1 | `shadow-session` | 0.986 | 0.000 | 0 | 0 | 0 | 0 | 0 | 0 | 2026-04-05 | 36 |  |
| 2 | `health-compendium` | 0.947 | 0.000 | 0 | 0 | 0 | 0 | 0 | 0 | 2026-03-30 | 43 |  |
| 3 | `pironman-pi5` | 0.932 | 0.000 | 0 | 0 | 0 | 0 | 0 | 0 | 2026-05-10 | 2 |  |
| 4 | `pi-ops` | 0.906 | 0.000 | 0 | 0 | 0 | 0 | 0 | 0 | 2026-03-30 | 43 | **A** |
| 5 | `claude-config` | 0.860 | 0.000 | 0 | 0 | 0 | 1 | 0 | 0 | 2026-03-30 | 43 | **A** |
| 6 | `findmy-bridge` | 0.851 | 0.000 | 0 | 0 | 0 | 0 | 0 | 0 | 2026-05-10 | 2 |  |
| 7 | `home-assistant` | 0.822 | 0.000 | 0 | 0 | 0 | 0 | 0 | 0 | 2026-03-30 | 43 |  |
| 8 | `CrossList` | 0.747 | 0.180 | 0 | 0 | 0 | 6 | 122 | 70 | 2026-03-30 | 43 |  |
| 9 | `exocortex` | 0.742 | 0.691 | 0 | 0 | 0 | 1 | 68 | 47 | 2026-05-10 | 2 |  |
| 10 | `code-reviewer` | 0.703 | 0.000 | 0 | 0 | 0 | 0 | 15 | 14 | 2026-05-10 | 2 |  |
| 11 | `fazio-core` | 0.697 | 1.000 | 0 | 0 | 0 | 0 | 5 | 5 | 2026-04-11 | 31 |  |
| 12 | `obsidian-mind` | 0.693 | 0.000 | 0 | 0 | 0 | 1 | 2 | 0 | 2026-04-07 | 35 |  |
| 13 | `gmail-ops` | 0.691 | 0.000 | 0 | 0 | 0 | 2 | 45 | 32 | 2026-05-06 | 6 |  |
| 14 | `Fazio-Atlas` | 0.662 | 0.528 | 0 | 0 | 0 | 3 | 36 | 32 | 2026-04-23 | 19 | **A** |
| 15 | `deal-sniper` | 0.662 | 0.115 | 0 | 0 | 0 | 19 | 87 | 75 | 2026-03-30 | 43 | **A** |
| 16 | `linkedin-authority` | 0.660 | 0.167 | 0 | 0 | 0 | 0 | 30 | 25 | 2026-05-10 | 2 |  |
| 17 | `dashcam-slicer` | 0.655 | 0.804 | 0 | 0 | 0 | 2 | 56 | 45 | 2026-03-30 | 43 |  |
| 18 | `fazio-harvest` | 0.650 | 0.792 | 0 | 0 | 0 | 2 | 101 | 80 | 2026-03-30 | 43 | **A** |
| 19 | `llm-gateway` | 0.646 | 0.600 | 0 | 0 | 0 | 1 | 30 | 18 | 2026-04-04 | 38 |  |
| 20 | `valuebet-bot` | 0.645 | 0.060 | 0 | 0 | 0 | 13 | 67 | 67 | 2026-03-30 | 43 |  |
| 21 | `trading-bot-farm` | 0.640 | 0.656 | 0 | 1 | 0 | 22 | 358 | 265 | 2026-03-30 | 43 |  |
| 22 | `llm-monitor` | 0.630 | 0.273 | 0 | 0 | 0 | 2 | 55 | 41 | 2026-04-04 | 38 |  |
| 23 | `Merge` | 0.628 | 0.000 | 0 | 0 | 0 | 1 | 7 | 0 | 2026-03-30 | 43 |  |
| 24 | `Nexus` | 0.591 | 0.410 | 0 | 0 | 0 | 6 | 173 | 151 | 2026-03-30 | 43 |  |
| 25 | `trackhub` | 0.585 | 0.054 | 0 | 0 | 0 | 20 | 92 | 12 | 2026-03-30 | 43 |  |
| 26 | `pidash-v5` | 0.582 | 0.188 | 0 | 1 | 0 | 3 | 101 | 69 | 2026-03-30 | 43 |  |
| 27 | `zeroclaw` | 0.557 | 0.197 | 2 | 0 | 0 | 147 | 375 | 221 | 2026-03-30 | 43 |  |
| 28 | `faziofinance-v6` | 0.500 | 0.011 | 2 | 0 | 0 | 13 | 842 | 585 | 2026-04-23 | 19 |  |
| 29 | `job-ops` | 0.461 | 0.184 | 3 | 5 | 0 | 28 | 1492 | 471 | 2026-03-30 | 43 | **A** |
| 30 | `CUE` | 0.403 | 0.325 | 2 | 2 | 0 | 71 | 379 | 216 | 2026-05-07 | 5 |  |
| 31 | `git-setup` | 0.376 | 0.000 | 0 | 0 | 0 | 1 | 0 | 0 | 2026-03-30 | 43 |  |

## Top 5 — best architecture (Q score)

- **shadow-session** Q=0.986 — cycles=0, gods=0, complex_fns=0 (2026-04-05, age 36d)
- **health-compendium** Q=0.947 — cycles=0, gods=0, complex_fns=0 (2026-03-30, age 43d)
- **pironman-pi5** Q=0.932 — cycles=0, gods=0, complex_fns=0 (2026-05-10, age 2d)
- **pi-ops** Q=0.906 — cycles=0, gods=0, complex_fns=0 (2026-03-30, age 43d)
- **claude-config** Q=0.860 — cycles=0, gods=0, complex_fns=1 (2026-03-30, age 43d)

## Bottom 5 — worst architecture (Q score)

- **zeroclaw** Q=0.557 — cycles=2, gods=0, complex_fns=147 (2026-03-30, age 43d)
- **faziofinance-v6** Q=0.500 — cycles=2, gods=0, complex_fns=13 (2026-04-23, age 19d)
- **job-ops** Q=0.461 — cycles=3, gods=5, complex_fns=28 (2026-03-30, age 43d)
- **CUE** Q=0.403 — cycles=2, gods=2, complex_fns=71 (2026-05-07, age 5d)
- **git-setup** Q=0.376 — cycles=0, gods=0, complex_fns=1 (2026-03-30, age 43d)

## TIER-A focus (post-M3 critical paths) — FRESH 2026-05-12

| Project | Q (Linux 05-12) | Q (Win prior) | Δ% | Branch | Push | Status |
|---------|-----------------|---------------|-----|--------|------|--------|
| `pi-ops` | 0.849 | 0.906 | -6.3% | main | YES | rescan+push DONE |
| `claude-config` | 0.663 | 0.860 | -22.9% | main | YES | rescan+push DONE — Q drop investigare |
| `Fazio-Atlas` | 0.588 | 0.662 | -11.2% | feat/parity-pii-redaction | NO | commit locale, push deferred (feature branch) |
| `deal-sniper` | 0.635 | 0.662 | -4.0% | main | YES | rescan+push DONE |
| `fazio-harvest` | 0.639 | 0.650 | -1.6% | master | NO | commit locale, push deferred (parallel session LOCKED) |
| `job-ops` | 0.519 | 0.461 | +12.6% | refactor/modularity-q-restore | NO | baseline saved, commit deferred (lefthook+parallel session) |
| `browser-pool` | 0.699 | n/a | NEW | main | NO | initial baseline DONE, push deferred (parallel session LOCKED) |

Note: `Q (Linux 05-12)` = fresh rescan today via Linux binary v0.5.7. Δ% reflects 19+ days code drift, NOT Win/Linux binary parity issue (baselines were 19-43d stale).

### Outstanding push (3/7)

| Repo | Commit SHA | Reason hold |
|------|-----------|-------------|
| `browser-pool` | 7511be2 | PARALLEL-SAFETY lock |
| `Fazio-Atlas` | bc41c7f | feature branch — parallel session control |
| `fazio-harvest` | 46f8c28 | PARALLEL-SAFETY lock |
| `job-ops` | uncommitted | lefthook vitest active in parallel; baseline.json kept as unstaged modified |

## M3 impact analysis

M3 chain (browser-pool migration of consumers) merged on 2026-05-12 across Fazio-Atlas / deal-sniper / fazio-harvest / job-ops.
Baselines pre-date M3 work in most cases; expected post-M3 effect:

- **deal-sniper**: cross_module_edges should DROP (scraper-core extracted to browser-pool)
- **fazio-harvest**: minor (only 1 entry migrated, FB/IG deferred)
- **job-ops**: cross_module_edges should DROP (14/20 extractors via browser-pool)
- **Fazio-Atlas**: Qwen OAuth +643 LoC but isolated provider — Q should be stable

Trend confirmation requires fresh rescan with `sentrux` binary (currently blocked: Windows-only `.exe`).

## Remediation priorities (worst-Q TIER-A)

1. **job-ops** Q=0.461 — 3 cycles, 5 god files, 28 complex fns. Worst TIER-A. Mechanical-split sweep in flight (PR #58-#63 Wave 1.5).
2. **CUE** Q=0.403 — 2 cycles, 2 god files, 71 complex fns. Not TIER-A but harvest-heavy. Defer.
3. **zeroclaw** Q=0.557 — 147 complex fns. Cross-compile pipeline stable, refactor low priority.

## Stale baselines (>30d, n=22)

| Project | Date | Age (d) |
|---------|------|---------|
| `health-compendium` | 2026-03-30 | 43 |
| `pi-ops` | 2026-03-30 | 43 |
| `claude-config` | 2026-03-30 | 43 |
| `home-assistant` | 2026-03-30 | 43 |
| `CrossList` | 2026-03-30 | 43 |
| `deal-sniper` | 2026-03-30 | 43 |
| `dashcam-slicer` | 2026-03-30 | 43 |
| `fazio-harvest` | 2026-03-30 | 43 |
| `valuebet-bot` | 2026-03-30 | 43 |
| `trading-bot-farm` | 2026-03-30 | 43 |
| `Merge` | 2026-03-30 | 43 |
| `Nexus` | 2026-03-30 | 43 |
| `trackhub` | 2026-03-30 | 43 |
| `pidash-v5` | 2026-03-30 | 43 |
| `zeroclaw` | 2026-03-30 | 43 |
| `job-ops` | 2026-03-30 | 43 |
| `git-setup` | 2026-03-30 | 43 |
| `llm-gateway` | 2026-04-04 | 38 |
| `llm-monitor` | 2026-04-04 | 38 |
| `shadow-session` | 2026-04-05 | 36 |
| `obsidian-mind` | 2026-04-07 | 35 |
| `fazio-core` | 2026-04-11 | 31 |

## Next actions

1. DONE — `sentrux` Linux binary installed at `~/.local/bin/sentrux` (v0.5.7 upstream prebuilt).
2. DONE — fresh baseline on browser-pool (initial scan, Q=0.699).
3. DONE — TIER-A 7/7 rescanned, deltas tabulated above.
4. PENDING — push 3 outstanding commits when parallel sessions release locks.
5. INVESTIGATE — `claude-config` Q drop -22.9% (sus large) and `job-ops` Q gain +12.6% (modularity refactor working?). Compare per-file deltas next session.
6. PROPAGATE — rescan remaining 24 non-TIER-A repos to refresh full ranking table.