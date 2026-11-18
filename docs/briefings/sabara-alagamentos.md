# Briefing: sabara-alagamentos

- Status: aprovado
- Data: 2026-11-17
- Aprovação: parcial em 2026-11-17; único ajuste pedido foi incluir alerta por SMS. As demais premissas deste texto permanecem.
- Repositório sugerido: `sabara-alagamentos`
- Squad previsto: squad padrão (modo subagentes), até o arquiteto definir donos de arquivos

## Problema

Moradores de Sabará (MG) convivem com alagamentos e inundações recorrentes, sobretudo nas áreas baixas do Rio das Velhas e do Rio Sabará. A informação existe, mas está espalhada: mapas antigos de risco, notícias e painéis nacionais de chuva e nível de rio. Não há um lugar único, em linguagem simples, que mostre onde a cidade costuma alagar e o que os sensores públicos estão indicando agora.

Referências públicas usadas neste rascunho, para o arquiteto conferir antes de desenhar o mapa:

- Mapeamento citado pelo Estado de Minas (18/12/2022), com base em ANA e CPRM: os piores setores junto ao Rio das Velhas estão em Vila Real, Catita, Caieiras, Centro e Rosário; no Rio Sabará, no Centro. O mesmo texto estima cerca de 460 edificações e 2.300 pessoas nesses setores.
- Carta e delimitação de áreas de risco do SGB/CPRM para Sabará (ação emergencial de 2012 e carta de suscetibilidade de 2015), publicadas no RiGeo.
- Em março de 2026, a imprensa registrou estado de emergência no município, com monitoramento da Defesa Civil em Roças Grandes e Rosário, junto ao Rio das Velhas.
- CEMADEN publica chuva e, onde há estação, nível de rio no Mapa Interativo. Ainda não foi conferido quais estações cobrem Sabará e o trecho a montante (Raposos, Rio Acima, Nova Lima).

Este produto não substitui a Defesa Civil. O SMS do MVP é aviso voluntário do próprio serviço, não alerta oficial do município.

## Público

Primário: morador de Sabará que precisa saber, antes de sair ou durante a chuva, se o seu bairro está entre os trechos que costumam alagar e se a chuva ou o rio estão subindo.

Secundário: quem acompanha a cidade (imprensa local, liderança de bairro) e quer a mesma leitura, sem painel operacional de emergência.

A Defesa Civil e a prefeitura não são usuárias do MVP. O SMS não é canal oficial de aviso.

## Proposta de valor

Um mapa web, aberto e leve, só de Sabará: a lista dos trechos historicamente críticos e, ao lado, a leitura atual da chuva (e do nível do rio, se houver estação pública utilizável). Quem quiser, cadastra o celular e o bairro e recebe um SMS quando a leitura daquele recorte ultrapassa o limite. A pessoa acompanha o próprio bairro sem cruzar vários sites.

## Escopo do MVP

1. Mapa de Sabará com os bairros e trechos citados nas fontes públicas acima, nomeados com clareza. Polígono oficial só entra se a licença do dado do SGB/CPRM permitir; senão, o MVP marca o bairro e aponta a fonte, sem desenhar uma mancha inventada.
2. Painel da condição atual: chuva recente das estações CEMADEN que cubram o município ou o Rio das Velhas a montante. Nível do rio só se a estação e o termo de uso estiverem confirmados.
3. Texto fixo em toda tela: isto não é alerta da Defesa Civil; em risco, o morador usa os canais oficiais do município.
4. Página curta de fontes, com data de cada camada, para o dado não parecer “ao vivo” quando for mapa estático.
5. Uso no celular. O mapa é aberto, sem login. O SMS pede só o celular e os bairros do MVP que a pessoa quer acompanhar.
6. Alerta por SMS, com adesão e cancelamento voluntários. A mensagem sai quando a leitura pública daquele bairro (chuva ou nível do rio, se houver estação) ultrapassa o limite que a arquitetura definir. Cada SMS diz que não é aviso da Defesa Civil e como cancelar. Sem adesão, sem mensagem. O limite numérico e o provedor de envio ficam para a decisão de arquitetura.

## Fora de escopo

- Push, sirene ou qualquer aviso que se apresente como sendo da Defesa Civil.
- Previsão de enchente, modelo hidrológico ou nota de risco calculada pelo sistema.
- Relato de morador, foto e qualquer dado pessoal além do celular e dos bairros escolhidos para o SMS.
- Deslizamento e movimento de massa, mesmo sendo um risco real em outros bairros de Sabará.
- Outros municípios, aplicativo nativo e painel interno para a prefeitura.
- Sensor próprio, câmera ou dado que não seja público.

## Métricas de sucesso

O MVP está válido quando uma pessoa, no celular, abre o mapa, localiza o próprio bairro na lista de trechos críticos e vê a chuva mais recente com a hora da medição e a fonte. No mesmo fluxo, ela adere ao SMS com o celular e o bairro, recebe uma mensagem quando o limite é ultrapassado e consegue cancelar. O aviso de que não substitui a Defesa Civil aparece em toda tela e em toda mensagem.

Não há meta de audiência neste rascunho.

## Riscos

- Tratar mapa de suscetibilidade como se fosse alagamento acontecendo agora. A interface precisa separar “histórico / suscetível” de “leitura do sensor agora”.
- Estação CEMADEN inexistente, fora do ar ou longe demais do bairro. O MVP precisa dizer “sem leitura” em vez de inventar um número.
- Licença dos vetores do SGB/CPRM pode impedir republicar o polígono. O contorno do MVP é a lista de bairros com fonte, não o arquivo geo.
- Confiança indevida: alguém deixar de procurar a Defesa Civil porque o mapa ou o SMS “parece tranquilo”, ou tratar a mensagem como ordem oficial.
- SMS que dispara sem evento, ou que não chega quando o limite foi ultrapassado. O texto precisa deixar claro o que a leitura mediu e a hora.
- Celular é dado pessoal. A adesão é consentimento, a finalidade é só este aviso, o cancelamento tem de funcionar, e o número não segue para outro uso.
- Custo e falha do provedor de SMS. Sem provedor confirmado na arquitetura, o envio não entra em produção.
- Chuva a montante (Raposos, Itabirito, Rio Acima) sobe o Rio das Velhas em Sabará com atraso. Mostrar ou avisar só com o pluviômetro local pode subestimar a cheia.

## Premissas deste rascunho

- Ferramenta cívica independente, repositório público, sem parceria formal com a prefeitura.
- Squad padrão, fluxo issue para PR, uma pessoa aprovando: o Mateus.
- Nome do repositório: `sabara-alagamentos`.
- O alerta do MVP é SMS voluntário e informativo, disparado por limite de leitura pública, nunca como canal da Defesa Civil.

## Perguntas em aberto

1. O público primário é o morador, como assumido aqui, ou a Defesa Civil?
2. Relato de quem está na rua entra depois do MVP ou nunca?
3. O repositório nasce público?
4. O nome `sabara-alagamentos` fica?

Resolvida nesta aprovação: o produto avisa por SMS. O aviso é do serviço, com adesão voluntária, e não é alerta oficial.

## Pontos de aprovação antes de criar o repositório

1. Este briefing, aprovado em 2026-11-17 com alerta por SMS no MVP.
2. Arquitetura: stack, pastas e dono de cada área, em `docs/decisions/`, com nova parada.
3. Confirmação explícita de nome, visibilidade e descrição para o `scaffolder` criar `metaus-hq/sabara-alagamentos` a partir do `squad-template`.
4. PR de setup sem merge, e só então o registro passa de ideia para em desenvolvimento.
