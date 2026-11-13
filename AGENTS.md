# Contexto do projeto

Site do **Câmbio Figueredo** — casa de câmbio, com cotações e pedidos.

O usuário fala português — responda sempre em português.

## Como este site é feito

É um **site de arquivo único**: todo o HTML, CSS e JavaScript estão dentro de
`index.html`. Não há build, nem `package.json`, nem framework. Para alterar,
edite o próprio `index.html`.

Ao lado dele ficam só arquivos de apoio:

- `logo.png` — a logo (também é a imagem do link compartilhado). Não volte a embutir em
  base64 no HTML: pesava 80 KB.
- `robots.txt` e `sitemap.xml` — para o Google.
- `.htaccess` — faz o `index.html` nunca ficar preso no cache do navegador (a Hostinger
  respeita). Sem isso, correção publicada demora a chegar em quem já visitou.

## A cotação na tela do cliente (cuidado: é dinheiro)

A cotação fica guardada no aparelho do cliente (`localStorage`) e é reconferida na nuvem
ao carregar, ao voltar para a aba e a cada 5 min. Já deu prejuízo quando ficava velha.
Regras que não podem ser quebradas:

- Estados em `cotEstado`: `verificando` (consultando, **sem** aviso), `ok`, `falhou`
  (só depois de duas tentativas; aí aparece o aviso amarelo).
- Enquanto está `verificando` e o valor guardado é de **outro dia**, os números ficam
  borrados e o botão de pedido espera — o cliente não pode ler nem tirar print de valor velho.
- Se a biblioteca do Supabase (CDN) não carregar, a cotação é buscada direto na API REST.
- Não mostre aviso antes de a primeira consulta terminar: ele piscava a cada abertura e
  parecia que o site estava quebrado.
- A mensagem do WhatsApp **não** leva cotação nem data (pedido do dono). Só leva uma linha
  de atenção quando a cotação não pôde ser confirmada.

## Onde está no ar

Domínio: **cambio-figueredo.com.br**

Hospedagem: Hostinger. Publicar = `git push` para `main`.

## Banco de dados

Supabase `xqiujdwvmbaipxyzcpvt.supabase.co`, acessado direto do navegador pela biblioteca carregada por
script. A chave que aparece no arquivo é a **pública (anon)** — é assim que
tem que ser; a proteção real são as regras de acesso (RLS) no banco.

**Nunca coloque a `service_role`, senha de banco ou qualquer token secreto
neste arquivo** — ele é servido para qualquer visitante.

Tabelas usadas: `cambio_cotacao`, `cambio_operacoes`, `cambio_pedidos`

- `cambio_pedidos` é a fonte da verdade do painel: a lista **e** os totais do "Resumo"
  saem dela.
- `cambio_operacoes` é só um espelho histórico — o site **grava** nela quando um pedido é
  aprovado, mas nunca lê. Não volte a ler essa tabela para montar o Resumo (era o que
  deixava o painel lento).

**Atenção: este repositório é PÚBLICO.** Qualquer pessoa vê o código. Redobre o cuidado com o que é escrito no arquivo.

## Convenções

- Identidade do git: `cicerobn <299460670+cicerobn@users.noreply.github.com>`.
- Mensagens de commit e comentários em português, explicando o efeito e o porquê.
- Antes de publicar, abra o arquivo no navegador e confira clicando — não há
  verificação automática neste tipo de projeto. Teste em tela de **celular** (é como os
  clientes usam) e, mexendo na cotação, teste também com a rede lenta e sem rede.
- Ao testar pedido, **não grave pedido de verdade**: ele aparece no painel do dono.
  Intercepte o `POST` em `cambio_pedidos` e o `window.open` do WhatsApp.
- O dono quer respostas curtas e diretas no chat.
