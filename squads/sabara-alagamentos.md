# Squad: sabara-alagamentos

## Missão
Entregar o mapa de trechos críticos de Sabará e o SMS voluntário, no ciclo plano aprovado, implementação, testes, revisão e PR.

## Produtos atendidos
- sabara-alagamentos (repositório ainda não criado)

## Composição
| Papel | Função | Dono de |
|---|---|---|
| lead | coordena e conversa com o Mateus | — |
| planner | quebra a demanda e define critérios de aceite | — |
| dev-back | API, ciclo, CEMADEN, SMS, adesão e catálogo | `api/`, `data/bairros.json` |
| dev-front | mapa, formulário e textos de aviso | `web/` |
| tester | escreve e roda testes | `tests/` |
| reviewer | revisa, somente leitura | — |

## Modo de trabalho
Subagentes em sequência, como no squad padrão. A API e o mapa compartilham o contrato do catálogo; time paralelo só depois desse contrato aceito.

## Regras específicas
- Seguem a ADR 0001 enquanto ela estiver em proposta ou aceita.
- SMS de produção permanece desligado até existir limite aprovado por bairro, token do CEMADEN e credencial do provedor.
- Nenhum agente inventa polígono de alagamento nem número de milímetros.
