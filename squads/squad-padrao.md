# Squad padrão de desenvolvimento

## Missão
Entregar o produto em ciclos curtos: plano aprovado → implementação → testes → revisão → PR.

## Composição
| Papel | Função | Dono de |
|---|---|---|
| lead (sessão principal) | coordena e conversa com o Mateus | — |
| planner | quebra a demanda e define critérios de aceite | — |
| dev-back / dev-front | implementam | arquivos de sua área (sem sobreposição) |
| tester | escreve e roda testes | pasta de testes |
| reviewer | revisa, somente leitura | — |

## Modo 1: subagentes (padrão, mais barato)
Fluxo sequencial na sessão do produto:
> Use o planner para planejar [tarefa]. Pare para minha aprovação.
Depois de aprovar: dev → tester → reviewer → PR.

## Modo 2: Agent Teams (experimental, mais caro)
Use quando houver módulos independentes. Ative CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1
no settings.json (em env) ou no ambiente. Exemplo de pedido:
> Crie um time com 3 teammates: dev-back (dono de /api), dev-front (dono de /web)
> e tester (dono de /tests). Use Sonnet em cada um. Cada um só edita seus arquivos.
> Quero aprovar o plano antes de qualquer implementação.
No Windows com VS Code, use o modo in-process (padrão).

## Regras do squad
- Nada vai para a main sem Pull Request e aprovação do Mateus.
- Dois agentes nunca editam o mesmo arquivo.
- Dúvida de requisito ou arquitetura: parar e perguntar.
