# Estoque Maria Formiga

Controle de cookies da **Doceria Maria Formiga** — um app de uma página, feito para
ser usado com uma mão no celular, do jeito que uma planilha funcionaria se ela
tivesse sido desenhada para o balcão.

![Cores e identidade tiradas do logo da doceria](assets/logo-mark.jpg)

## O que dá para fazer

- **Estoque** — um cartão por sabor com a quantidade em número grande, preço,
  valor parado na prateleira e um selo de situação (`Ok`, `Acabando`, `Acabou`).
  - `− Vendi 1` e `+ Entrou 1` lançam na hora. **Segurando o botão** ele repete
    rápido, e tudo é agrupado em **um único lançamento** ao soltar.
  - Tocar no número abre o teclado de lançamento: **Vender**, **Fornada** ou
    **Ajustar** (contagem certa), com prévia do antes → depois e do valor.
  - Cada lançamento mostra um aviso com **Desfazer**.
- **Planilha** — a mesma informação em tabela, com as células de quantidade,
  preço e mínimo editáveis direto, linha de total e exportação em CSV
  (`;` e vírgula decimal, abre no Excel, Numbers e Google Sheets).
- **Histórico** — todos os lançamentos agrupados por dia, com o total vendido e
  o faturamento do dia. Apagar um lançamento devolve a quantidade ao estoque.
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
- Todas as cores da interface são variáveis CSS no `:root` (e no bloco escuro).
