# metaus-hq / hq — a fábrica

Repositório central da organização **metaus-hq**. Aqui nascem e são coordenados os
produtos. O desenvolvimento de cada produto acontece no repositório do próprio produto.

## Responsabilidades do HQ
- Transformar ideias em briefings e decisões de arquitetura
- Criar os repositórios dos produtos a partir de `metaus-hq/squad-template`
- Manter o `registry.md` (lista de produtos, status e squad responsável)
- Manter a definição dos squads em `squads/`

## Time de gestão (subagentes em .claude/agents/)
- product-manager: escreve o briefing do produto
- architect: propõe stack e arquitetura (ADR)
- scaffolder: cria o repositório do produto e prepara o primeiro commit
- docs: mantém registry, squads e documentação

## Fluxo para criar um produto
1. Mateus descreve a ideia.
2. product-manager escreve docs/briefings/<produto>.md e PARA para aprovação.
3. architect propõe stack e estrutura e PARA para aprovação.
4. scaffolder cria o repositório (nome e visibilidade confirmados com o Mateus) e abre PR de setup.
5. docs registra o produto no registry.md via PR.
6. Mateus abre a pasta do produto em uma nova janela do VS Code e aciona o squad dele.

## Regras
- Nunca criar, apagar ou alterar visibilidade de repositório sem aprovação explícita do Mateus.
- Todo produto nasce de metaus-hq/squad-template.
- Nomes de repositório em kebab-case, minúsculas.
- Mudanças neste repositório entram por Pull Request; o merge é do Mateus.
- Nunca ler, editar ou commitar .env ou segredos.
- Em dúvida de escopo, nome ou arquitetura: perguntar antes de agir.

## Organização do computador
Os repositórios ficam lado a lado numa pasta de trabalho:
<pasta-de-trabalho>/hq, <pasta-de-trabalho>/squad-template, <pasta-de-trabalho>/<produto>
O scaffolder cria os produtos na pasta acima do hq (../<produto>).
