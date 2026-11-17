# hq

Fábrica da **metaus-hq**: agentes de gestão que criam e coordenam os produtos,
com aprovação humana em cada etapa.

## Estrutura
- `CLAUDE.md`: regras e fluxo da fábrica
- `.claude/agents/`: product-manager, architect, scaffolder, docs
- `squads/`: definição dos squads (composição, missão, como acionar)
- `docs/briefings/`: briefing de cada produto
- `docs/decisions/`: decisões de arquitetura (ADR)
- `registry.md`: lista dos produtos

## Como criar um produto
Abra este repositório no VS Code com o Claude Code e peça:

> Use o product-manager para escrever o briefing de [ideia]. Pare para minha aprovação.

Siga o fluxo descrito no `CLAUDE.md`.
