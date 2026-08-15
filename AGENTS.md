# Contexto do projeto

Site do **Câmbio Figueredo** — casa de câmbio, com cotações e pedidos.

O usuário fala português — responda sempre em português.

## Como este site é feito

É um **site de arquivo único**: todo o HTML, CSS e JavaScript estão dentro de
`index.html`. Não há build, nem `package.json`, nem framework. Para alterar,
edite o próprio `index.html`.

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

**Atenção: este repositório é PÚBLICO.** Qualquer pessoa vê o código. Redobre o cuidado com o que é escrito no arquivo.

## Convenções

- Identidade do git: `cicerobn <299460670+cicerobn@users.noreply.github.com>`.
- Mensagens de commit e comentários em português, explicando o efeito e o porquê.
- Antes de publicar, abra o arquivo no navegador e confira clicando — não há
  verificação automática neste tipo de projeto.
