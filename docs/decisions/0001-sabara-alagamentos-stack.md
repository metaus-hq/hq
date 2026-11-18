# ADR 0001: Stack e estrutura de sabara-alagamentos

- Status: proposta
- Data: 2026-11-17

## Contexto

O briefing aprovado pede um mapa web de Sabará, a leitura pública de chuva (e de nível, se houver estação) e um SMS voluntário quando essa leitura ultrapassa um limite. O mapa não pode desenhar mancha de alagamento sem dado licenciado. O SMS não é alerta da Defesa Civil.

A máquina de trabalho tem toolchain de Python instalada no editor. O produto precisa de um processo que continue consultando a fonte mesmo com o site fechado, porque o SMS não pode depender de alguém estar com o mapa aberto.

O caminho público conhecido para leitura contínua do CEMADEN é o webservice com token obtido por cadastro (o Mapa Interativo mostra os dados, mas não é a interface de um serviço). Isso precisa ser confirmado no cadastro antes de existir cliente de produção. Até lá, a tela diz "sem leitura".

## Decisão

Um processo Python 3.12, com FastAPI, serve o mapa e o formulário e roda o ciclo de leitura. PostgreSQL guarda adesões e o histórico mínimo para não repetir SMS. O mapa é uma página única, HTML e Leaflet, com tiles do OpenStreetMap. Sem SPA.

Módulos, nesta ordem de dependência:

1. Catálogo de bairros do briefing, com nome, fonte e ponto aproximado. Sem polígono inventado.
2. Cliente CEMADEN atrás de uma interface. Credencial só em variável de ambiente. Se não houver token, estação ou leitura fresca, o resultado é "sem leitura".
3. Avaliador de limite. O número não fica no código. Fica em configuração por bairro. Sem número aprovado para aquele bairro, não há SMS.
4. Adesão: celular em E.164, bairros escolhidos, instante do consentimento e código de cancelamento. Cancelar apaga o número.
5. Mensageiro, com Twilio como primeiro adaptador. Zenvia entra no mesmo contrato se a entrega ou o custo no Brasil for melhor. `SMS_ENABLED` nasce falso. Produção só liga com token do CEMADEN, limite aprovado e credencial do provedor.
6. Ciclo a cada 10 minutos. Uma mensagem por bairro no máximo a cada 6 horas enquanto a leitura seguir acima do limite. Nova sequência só depois de a leitura voltar abaixo. Leitura mais velha que 30 minutos não dispara. O texto leva o valor, a hora em America/Sao_Paulo, a fonte CEMADEN, a frase de que não é a Defesa Civil e o modo de cancelar.

O limite numérico desta proposta é nenhum. Escolher milímetros ou cota sem a série da estação real dispararia aviso errado. O número entra numa revisão desta ADR, depois de ver a estação que cobre cada bairro.

### Pastas e donos

| Pasta | Dono | Conteúdo |
|---|---|---|
| `api/` | dev-back | rotas, ciclo, CEMADEN, SMS, adesão, banco |
| `data/bairros.json` | dev-back | catálogo canônico, lido pela API |
| `web/` | dev-front | página do mapa, formulário e textos de aviso |
| `tests/` | tester | critérios de aceite e bordas, sem alterar produção |

O front não edita `data/bairros.json`. Ele consome o catálogo pela API. Dois agentes não editam o mesmo arquivo.

Modo do squad: subagentes em sequência. O contrato entre mapa e API ainda é um só. Time paralelo fica para quando esse contrato estiver aceito.

## Alternativas consideradas

- Next.js e Node num serviço só. Serve o mesmo desenho, mas a toolchain já presente na máquina é Python.
- Página estática sem servidor. Não envia SMS nem consulta a fonte com o site fechado.
- Raspar o Mapa Interativo. Quebra sem aviso e não é o caminho de uso do webservice.
- Limite fixo de chuva no código, por exemplo 30 mm em 1 hora. Parece decisão e é chute. Fica de fora até haver estação e série.

## Consequências

- O repositório, quando for criado, nasce com `api/`, `web/`, `data/` e `tests/`, mais o `CLAUDE.md` preenchido com estes comandos: instalar com `pip install -e .`, rodar com `uvicorn`, testar com `pytest`.
- Segredos (token CEMADEN, Twilio, banco) só em ambiente, nunca no git.
- SMS real permanece desligado até a revisão que gravar o limite de cada bairro.
- O mapa separa visualmente "trecho histórico" de "leitura de agora".
- Risco que permanece: chuva a montante pode encher o Rio das Velhas sem o pluviômetro local ter passado do limite. O texto do SMS não pode soar como previsão nem como ordem de saída.
