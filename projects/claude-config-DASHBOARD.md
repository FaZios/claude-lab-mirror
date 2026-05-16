# Dashboard — claude-config
_Auto-generato da dashboard-keeper · Ultimo refresh: 2026-05-13 14:30_

## Status

| Campo | Valore |
|---|---|
| Stato | PROD-STABLE |
| Stack | Bash · Python · YAML · config rules (no runtime, infra config) |
| Repo | github.com/FaZios/claude-config (privato) |
| Branch attivo | main |
| Avanzamento | ~85% (S1 5/5 done 2026-05-13, 3 pending user actions) |

## Attivita ultimi 30g

- Commit: 127
- Ultimo commit: `3181ad3` fix(bridge): HTTPS clone + gh auth token fallback for PAT (2026-05-13)

## Code metrics

- LoC: n/a (config, scripts bash/python, regole markdown)
- Test: n/a
- Sentrux Q: 8.598/10.000 (audit 2026-03-30 — 2 file lunghi + 1 fn)

## Dipendenze interne (cross-progetto)

| Direzione | Progetto | Nota |
|---|---|---|
| Servisce | tutti i progetti | regole globali CLAUDE.md, skills, ADR, deploy scripts |
| Contiene ADR per | browser-pool | ADR-0001 engine-pluggable + ADR-0002 antibot-sota |

## Deploy state

- Pi5: not-deployed (config repository)
- Host: `~/.claude/` su tutti i device (PC, Book4, Pi5)
- Healthcheck: n/a

## Open gaps

- **[PENDING USER]** claude-lab-mirror repo provisioning (S1 action utente)
- **[PENDING USER]** Book4 drift verify (S1 action utente)
- **[WATCH]** Sentrux 0.6.x upstream watch (S1 action utente)
- **[ARCH]** 2 file > 500 righe: `docs/superpowers/plans/2026-03-27-webauthn-biometric-auth.md` (1571), `skills/skill-rules.json` (1226). Nota: docs ignorabili se non modificati
- **[MEMORY]** Sistema `memory/` DEPRECATO — ora `~/pi-ops/OPS-LOG.md` + `RUNBOOKS.md`

## Prossimi passi suggeriti

1. **claude-lab-mirror** — provisioning repo (azione utente pendente da S1)
2. **Book4 drift** — verificare drift rispetto a PC config (azione utente pendente)
3. **Sentrux 0.6.x** — watch per upstream release (watch passivo)
