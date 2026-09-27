# Changelog

## 0.3.0 — routed dual-engine architecture

### Changed
- task classification moved to the beginning of the Skill;
- analysis of existing arguments and construction of new arguments now use separate engines;
- binary logic diagrams are no longer forced as the default topology;
- the main SKILL.md was shortened and now delegates detailed probability/audit rules to references.

### Added
- `references/task-router.md`;
- `references/probabilistic-argument.md`;
- `references/source-trace-map.md`;
- explicit Source Trace Map relations: `direct`, `synthesized`, `inference`, `gap`;
- topology selection guidance for causal, parallel, binary, merge, and feedback structures;
- routed output templates for Reconstruction, Probability, and Mixed tasks.

### Reliability
- source-derived claims, analytical reconstruction, critique, and external evidence are explicitly separated;
- logic gaps remain gaps instead of being silently repaired to make a cleaner diagram;
- detailed probability rules are maintained in one reference instead of duplicated in SKILL.md and logic-audit.md.

## 0.2.0 — probabilistic argumentation

- minimum-sufficient argument;
- claim-strength calibration;
- decisive-variable reversal test;
- evidence hierarchy;
- strongest-counterargument handling;
- stopping rules.

## 0.1.0 — initial logic clarifier

- mother question;
- core thesis;
- old-model/new-model reconstruction;
- mechanism chains;
- logic audit;
- reusable framework compression.
