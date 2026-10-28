# Carona Solidária

> **Iniciativa encerrada.** O site funcionou de 22 a 26 de outubro de 2026, para o 2º turno das eleições (25/10/2026), e saiu do ar depois disso. Este repositório fica como registro e como ponto de partida para uma próxima edição.

Site simples para vizinhos com carro levarem vizinhos com dificuldade de locomoção (idosos, pessoas com deficiência) até o local de votação. Gratuito e apartidário. Funcionou em **Natal**, **Recife** e **João Pessoa**: a pessoa escolhia a cidade na primeira tela.

Criado e organizado por **Ricardo Rodrigues** ([@rsilveirafh](https://github.com/rsilveirafh)).

## Por que existiu

Muitos idosos da Vila de Ponta Negra (Natal/RN) deixaram de votar no 1º turno por falta de transporte. A ideia foi juntar quem precisava de carona com vizinhos dispostos a levar, sem partido, sem dinheiro envolvido e sem guardar dados depois da eleição.

## Linha do tempo

| Data | O que aconteceu |
|---|---|
| 19/10/2026 | Primeira versão do site, só para a Vila de Ponta Negra: passo a passo para quem pede carona, cadastro de motorista e mapa. |
| 22/10/2026 (manhã) | Site ligado à planilha (Google Apps Script), lista oficial de locais de votação do TSE, aprovação de motoristas, senha por aparelho, limites contra robôs, exclusão automática dos dados e avisos por e-mail. |
| 22/10/2026 (tarde) | Ampliado da Vila de Ponta Negra para **toda Natal**. Recife e João Pessoa ganham sites próprios, cada um numa organização do GitHub: `caronasolidaria-recife` e `caronasolidaria-jp`. |
| 23/10/2026 (madrugada) | As três cidades viram **um site único** em `caronasolidaria.github.io`, com escolha de cidade (`?cidade=natal`, `?cidade=recife`, `?cidade=jp`) e uma planilha por cidade. Os endereços de Recife e João Pessoa passam a só redirecionar, levando junto o cadastro de motorista guardado no celular. Cards de divulgação para stories. |
| 25/10/2026 | 2º turno. Dia das caronas, das 8h às 17h. |
| 26/10/2026, 18h | Dados apagados automaticamente nas três planilhas. A partir daí o script não aceita mais pedidos. |
| 27/10/2026 | Encerramento: as organizações `caronasolidaria-recife`, `caronasolidaria-jp` e `caronasolidaria` foram excluídas do GitHub, e este repositório foi transferido para `rsilveirafh/carona-solidaria`, sem GitHub Pages (o site não está mais no ar). Cards de agradecimento. |

## Números finais

Contados pelos e-mails de aviso, já que as planilhas foram apagadas no prazo:

| Cidade | Motoristas cadastrados | Pedidos de carona |
|---|---:|---:|
| Natal | 10 | 7 |
| Recife | 16 | 2 |
| João Pessoa | 18 | 4 |
| **Total** | **44** | **13** |

Nenhuma carona foi devolvida para a lista depois de assumida. O número de caronas efetivamente realizadas não ficou registrado (os e-mails só avisavam pedido novo, motorista novo e carona devolvida, e as planilhas foram apagadas).

## Endereços e repositórios

Tudo isto deixou de existir em 27/10/2026:

| Antes | Papel | Destino |
|---|---|---|
| `caronasolidaria/caronasolidaria.github.io` → <https://caronasolidaria.github.io/> | site único das três cidades | repositório transferido para **`rsilveirafh/carona-solidaria`** (este); Pages desligado; organização `caronasolidaria` excluída |
| `caronasolidaria-recife/caronasolidaria-recife.github.io` → <https://caronasolidaria-recife.github.io/> | site de Recife (22/10) e depois só redirecionamento | repositório e organização excluídos |
| `caronasolidaria-jp/caronasolidaria-jp.github.io` → <https://caronasolidaria-jp.github.io/> | site de João Pessoa (22/10) e depois só redirecionamento | repositório e organização excluídos |

Os sites de Recife e João Pessoa eram cópias do site de Natal com outra configuração de cidade; tudo o que eles tinham foi incorporado aqui no site único de 23/10, então nada se perdeu com a exclusão.

As URLs do Apps Script em `config.js` continuam no código só como registro: depois de 26/10/2026, 18h, o script recusa qualquer pedido.

## Divulgação

- `divulgacao/opcao-1.png` a `opcao-3.png`: cards para stories (1080×1920), usados antes da eleição.
- `divulgacao/agradecimento/card-1.png` a `card-4.png`: carrossel de agradecimento (1080×1350), depois da eleição.

---

## Como funcionava

- **Site**: estático, no GitHub Pages (`index.html`, `app.js`, `config.js`).
- **Dados**: **uma planilha Google privada por cidade**, cada uma acessada só pelo seu Apps Script (`apps-script/Code.gs`, com `NOME_CIDADE` da cidade). O site escolhia a planilha pela cidade (`CIDADES` no `config.js`). **Nenhum dado pessoal fica neste repositório.**
- **Locais de votação**: `locais-natal.json` (496, Grande Natal), `locais-recife.json` (1.048, Grande Recife) e `locais-jp.json` (349, Grande João Pessoa), do 2º turno de 2026, tirados dos [dados abertos do TSE](https://dadosabertos.tse.jus.br/) (eleitorado — locais de votação).
- **Mapa**: [OpenStreetMap](https://www.openstreetmap.org/copyright), com [Leaflet](https://leafletjs.com/) e busca de endereços pelo Nominatim.

1. Quem precisa de carona responde um passo a passo (uma pergunta por tela, letra grande), marca a casa no mapa e escolhe o local de votação na lista oficial.
2. Motoristas voluntários fazem o próprio cadastro (carro, lugares, cadeira de rodas, de onde saem, horário). O cadastro fica **pendente** até a organização aprovar. Aprovado, o motorista vê os pedidos ordenados por distância, só com rua/bairro, local de votação, horário e necessidades.
3. Ao tocar em "Eu levo", o pedido sai da lista e só esse motorista vê nome, WhatsApp e endereço, com botões para chamar no WhatsApp, ir até a casa e seguir até o local de votação.
   Com o painel aberto, a lista se atualiza sozinha a cada 2 minutos (e ao voltar para a página), avisando e vibrando quando chega pedido novo.
4. O mapa da página inicial mostra só a **região aproximada** (~450 m) de pedidos e motoristas. Os locais de votação, que são prédios públicos, aparecem na posição exata.

A planilha de cada cidade era o painel da organização: aba `Pedidos` (quem pediu, quem assumiu e quando) e aba `Motoristas`.

## Para reutilizar numa próxima eleição

1. Atualize as datas: `DATA` e `APAGAR_ATE` no `config.js`, `APAGAR_EM` no `Code.gs`.
2. Troque os arquivos `locais-*.json` pelos locais de votação da nova eleição (dados abertos do TSE).
3. Crie uma planilha nova por cidade (passo a passo abaixo) e coloque as URLs novas em `CIDADES` no `config.js`.
4. Ajuste `REPOSITORIO`, `CONTATO` e `CONTATO_NOME` no `config.js` e publique o site no GitHub Pages (**Settings → Pages → Deploy from a branch → `main` / raiz**). Os caminhos são relativos, então o site funciona tanto em `usuario.github.io` quanto em `usuario.github.io/carona-solidaria/`.

### Ligar a planilha de uma cidade (5 minutos, uma vez)

1. Abra <https://sheets.new> e dê um nome, ex.: `Carona Solidária — dados`.
2. Menu **Extensões → Apps Script**. Apague o conteúdo e cole o de `apps-script/Code.gs` (versão bruta: <https://raw.githubusercontent.com/rsilveirafh/carona-solidaria/main/apps-script/Code.gs>). Troque `NOME_CIDADE` pela cidade da planilha (vai no assunto dos e-mails) e salve.
3. No seletor de funções, escolha `setup` e clique em **Executar**. Autorize o acesso (aparece "app não verificado": *Avançado → Acessar*). As abas `Pedidos` e `Motoristas` serão criadas, e a exclusão automática dos dados fica agendada.
4. **Implantar → Nova implantação →** tipo **App da Web**:
   - Executar como: **Eu**
   - Quem pode acessar: **Qualquer pessoa**
5. Copie a URL que termina em `/exec` e coloque no `SCRIPT_URL` da cidade, em `CIDADES` no `config.js`.
6. Para uma cidade nova, copie uma entrada de `CIDADES` (nome, DDD, área do mapa, região da busca, exemplos e o arquivo de locais do TSE). `CONTATO` e `CONTATO_NOME` valem para todas as cidades.

> Se mudar o `Code.gs` depois, cole a versão nova, rode `setup` de novo e use **Implantar → Gerenciar implantações → editar (lápis) → Versão: Nova versão**, para manter a mesma URL.

## Exclusão dos dados

Para a segurança de todos, os dados eram apagados sozinhos no prazo (`APAGAR_EM` no `Code.gs` e `APAGAR_ATE` no `config.js`; nesta edição, 26/10/2026, às 18h):

- o `setup` agenda a exclusão de todas as linhas de `Pedidos` e `Motoristas`;
- como garantia extra, depois desse horário o script apaga tudo na primeira chamada que receber e não aceita mais pedidos.

O Google Planilhas guarda um **histórico de versões**. Para apagar de vez, depois do prazo, exclua o arquivo da planilha e esvazie a lixeira do Google Drive.

## Avisos por e-mail

O script manda um e-mail para a conta dona da planilha quando chega um **pedido novo**, quando um **motorista novo** espera aprovação e quando uma **carona é devolvida** para a lista. Os e-mails não levam nome, telefone nem endereço: só o número do pedido ou do motorista e o link da planilha. Para desligar, mude `AVISAR_POR_EMAIL` para `false` no `Code.gs`.

> Lição desta edição: como as planilhas são apagadas no prazo, os e-mails acabaram sendo o único registro dos números. Se quiser saber quantas caronas foram realizadas, anote a contagem de pedidos `realizado` antes do horário de exclusão.

## Aprovação dos motoristas (organização)

1. Na aba `Motoristas`, cada cadastro novo chega com `status` = `pendente`.
2. Confira a pessoa (nome, WhatsApp, carro) e escolha `ativo` no menu da coluna `status`. Ela passa a ver os pedidos ao tocar em **Atualizar** no site.
3. Para tirar alguém, escolha `inativo`.
4. **Motorista trocou de celular?** Por segurança, o acesso fica só no aparelho do cadastro. Apague a célula `token` dele: ele se cadastra de novo no celular novo, com o mesmo WhatsApp, e continua aprovado.

Para dividir a verificação com outras pessoas, compartilhe a planilha com elas como **editoras**. Elas passam a ver todos os dados: só pessoas de confiança da organização.

## Segurança

A URL do Apps Script fica no código do site (como em qualquer site), então todas as proteções estão no `Code.gs`:

- **Pedidos**: qualquer pessoa pode pedir carona, mas ninguém consegue ler os pedidos sem ser motorista aprovado.
- **Motoristas**: cada um recebe no cadastro uma senha secreta (`token`), guardada só no celular dele e exigida em todas as ações. Saber o WhatsApp de alguém não dá acesso a nada; não dá para recadastrar o WhatsApp de outra pessoa.
- **Antes de assumir**, o motorista vê só rua/bairro, local de votação, horário e necessidades. Nome, telefone e endereço completo só aparecem para quem assumiu.
- **Limites**: até 4 caronas combinadas por motorista; até 2 pedidos esperando motorista por WhatsApp; até 60 pedidos e 30 cadastros de motorista por hora (contra robôs).
- **Mapa aberto**: só contagens em regiões de ~450 m; nenhum nome, telefone ou endereço.
- **Planilha**: valores gravados como texto (nada vira fórmula; coordenadas não são corrompidas pela planilha em português).
- A busca de endereços envia o texto digitado ao OpenStreetMap (Nominatim).

## Código do grupo (opcional)

Por padrão, qualquer pessoa com o link pode se cadastrar como motorista (e espera a aprovação). Para restringir também o cadastro, preencha `CODIGO_MOTORISTAS` no `Code.gs` e publique uma nova versão: o site passa a pedir o código antes do cadastro, sem mudar nada no site.

## Cuidados

- **Não apague linhas** da planilha durante a operação (os números dos pedidos dependem disso). A coluna `status` tem um menu de opções: para cancelar um pedido, escolha `cancelado`; para tirar um motorista, escolha `inativo`. Depois de levar a pessoa, marque o pedido como `realizado`.
- Transporte de eleitores tem restrições legais (Lei nº 6.091/1974). O site traz avisos de que a iniciativa é apartidária e de que a organização só põe as pessoas em contato. Evite cores, textos ou apoios partidários e não aceite doações em dinheiro. Na dúvida, consulte o cartório eleitoral.
