# Estoque Maria Formiga

Controle de cookies da **Doceria Maria Formiga** — um app de uma página, feito para
ser usado com uma mão no celular, do jeito que uma planilha funcionaria se ela
tivesse sido desenhada para o balcão.

![Cores e identidade tiradas do logo da doceria](assets/logo-mark.jpg)

## Senha

Na primeira vez o app pede para **criar uma senha de quatro números**; depois
disso é ela que abre o app. Fica destrancado por 12 horas em cada aparelho, e o
botão **Trancar o app** no rodapé fecha na hora.

A senha é guardada como hash SHA-256 — nunca em texto puro. Publicada como
Artifact, ela fica no banco e vale em qualquer aparelho; como arquivo local, vale
por aparelho.

> A senha é uma tranca contra quem abrir o endereço sem ser você, não um cofre:
> quem souber ler o código-fonte da página passa por ela. A proteção de verdade é
> o próprio link do Artifact, que só abre na conta da dona.

## Dois estoques por sabor

Cada sabor tem duas contagens separadas:

- **Pra vender** — assado, pronto na prateleira. É o que sai numa venda e o que
  entra na conta do valor em estoque.
- **Pra assar** — massa esperando o forno. Não conta como valor em estoque
  porque ainda não dá para vender.

Cada aba cuida de um lado:

| Onde | O que se faz |
| --- | --- |
| **Estoque** | vender (é a rotina do balcão) e corrigir o pra vender |
| **Planilha** | o controle do **pra assar**, e também do pra vender |

No cartão do Estoque o "pra assar" aparece só como número, para consulta — quem
mexe nele é a planilha. Quando o "pra vender" chega a zero mas ainda tem massa,
o selo do sabor avisa **Precisa assar** em vez de **Acabou**.

## O que dá para fazer

- **Estoque** — um cartão por sabor com as duas contagens em número grande,
  preço, valor na prateleira e selo de situação (`Ok`, `Acabando`,
  `Precisa assar`, `Acabou`). É a tela do balcão, com uma ação só:
  - `− Vendi 1` vende uma unidade. Toques seguidos são agrupados em **um único
    lançamento** (três toques = uma venda de 3), então o histórico não enche.
  - Tocar no número do **pra vender** abre o teclado para vender uma quantidade
    maior ou ajustar a contagem, com prévia do antes → depois e do valor antes
    de confirmar.
  - Cada lançamento mostra um aviso com **Desfazer**.
- **Planilha** — onde se controla o **pra assar**: pra vender, pra assar, preço
  e mínimo editáveis direto na célula, linha de total e exportação em CSV
  (`;` e vírgula decimal, abre no Excel, Numbers e Google Sheets).
- **Histórico** — todos os lançamentos agrupados por dia, com o total vendido e
  o faturamento do dia. Apagar um lançamento devolve as quantidades ao que eram.
  No fim da aba, **Limpar tudo e começar do zero** apaga o histórico e zera as
  contagens, mantendo sabores e preços — feito para depois de testar.
- **Sabores** — cadastrar, renomear, mudar preço, definir o mínimo que dispara o
  aviso de "acabando" e escolher a cor do sabor.

Começa com os quatro sabores da casa: Chocolatudo, Kinder, Nutella e Ninho.

## Onde os dados ficam

O arquivo funciona nos dois modos, sem configuração:

| Como você abre | Onde salva |
| --- | --- |
| Publicado como Artifact no Claude | Banco do Artifact — abre igual em qualquer aparelho |
| `index.html` direto no navegador ou no GitHub Pages | `localStorage` do próprio aparelho |

O rodapé do app sempre diz em qual dos dois está (`Salvo na nuvem` /
`Salvo neste aparelho`).

## Usar no iPhone

1. Abra o endereço no Safari.
2. Botão de compartilhar → **Adicionar à Tela de Início**.
3. Ele abre em tela cheia, com o selo da doceria como ícone, sem barra do
   navegador.

Para publicar de graça: **Settings → Pages → Branch: `main` → `/ (root)`** neste
repositório. O endereço fica `https://<usuario>.github.io/<repositorio>/`.

## Arquivos

```
index.html              o app inteiro — HTML, CSS e JS em um arquivo, sem dependências
manifest.webmanifest    nome, cores e ícone para instalar na tela de início
assets/logo.jpg         logo original da doceria
assets/logo-mark.jpg    selo usado no topo do app
assets/apple-touch-icon.jpg  ícone da tela de início
```

## Identidade visual

Tudo foi tirado do logo, amostrando as cores da própria imagem:

| Cor | Uso |
| --- | --- |
| `#E5C48E` creme | fundo (`#EDD9B2`) e cartões (`#FBF3E4`) |
| `#6E2B1C` bordô do "Maria" | acento, botões de venda |
| `#A56B3E` caramelo do "Formiga" | detalhes, links, quantidades pendentes |
| `#4C2212` café da formiga | texto |

Tipos: **Fraunces** nos números e títulos (a serifa retrô ecoa a do logo),
**DM Sans** na interface e **DM Mono** nas colunas da planilha.
Tem tema claro e escuro — acompanha o do aparelho.

## Mexer no código

Não tem build, nem dependência, nem passo de instalação: `index.html` é o app.
Abra no editor, edite, recarregue no navegador.

- Os sabores iniciais estão em `DA_CASA`.
- A paleta de cores de sabor está em `CORES`.
- Os campos de cada sabor são `qtd` (pra vender), `crus` (pra assar), `preco`,
  `minimo`, `cor` e `ordem`.
- Cada lançamento guarda `dVender` e `dAssar` — quanto mexeu em cada contagem —
  o que é o que permite desfazer e apagar sem recalcular nada.
- Todas as cores da interface são variáveis CSS no `:root` (e no bloco escuro).
