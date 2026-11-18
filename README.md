# Presell + P1 com layout dinâmico (ambiente de teste)

Várias presells mandam o lead para a **mesma P1**. A P1 lê a `utm_source` da URL e mostra o layout daquela presell (Layout 1, 2 ou 3).

## Arquivos

| Arquivo | O que é |
|---|---|
| [`presell.html`](presell.html) | **Presell** de teste: 2 perguntas e, no último passo, um painel para escolher qual `utm_source` mandar. |
| [`p1.html`](p1.html) | **P1**: URL única que troca o layout conforme a `utm_source` que chega. |
| [`index.html`](index.html) | Página inicial do teste, só com links para as duas. Não faz parte do funil. |

As duas partes são HTML puro, cada uma em um arquivo só: o CSS e o script ficam dentro do próprio arquivo, sem nenhum arquivo externo.

## Links (depois de ativar o GitHub Pages)

- Início: https://gabrielaacristofolini-hue.github.io/presell-teste-layout-dinamico-/
- Presell: https://gabrielaacristofolini-hue.github.io/presell-teste-layout-dinamico-/presell.html
- P1: https://gabrielaacristofolini-hue.github.io/presell-teste-layout-dinamico-/p1.html?utm_source=source2

## Ativar o GitHub Pages

**Settings → Pages → Build and deployment** → Source: **Deploy from a branch** → Branch: **main** e pasta **/ (root)** → **Save**. O site fica no ar em 1 a 2 minutos.

## Como a P1 escolhe o layout

| `utm_source` | Layout |
|---|---|
| `source1` | Layout 1 (azul) |
| `source2` | Layout 2 (verde) |
| `source3` | Layout 3 (laranja) |
| vazia ou desconhecida | Layout 1 (padrão) |

Maiúsculas não importam (`Source2` = `source2`). Essa tabela fica no `CONFIG`, no fim do `p1.html`.

## Adicionar uma operação nova (ex.: Layout 4)

1. No `p1.html`, copie um bloco `<template id="layout-3"> … </template>`, troque para `id="layout-4"` e `class="layout layout-4"`, e edite o HTML como quiser.
2. No CSS do `p1.html`, crie as cores: `.layout-4 { --cor: …; --cor-escura: …; --fundo: …; }`.
3. No `CONFIG.layoutPorSource`, adicione `minhasource: 'layout-4'`.
4. Na campanha do Google Ads, use no **sufixo do URL final**: `utm_source=minhasource`.

## Levando para a operação

- **Presells reais:** o botão final precisa levar até a P1 a `utm_source` que chegou do Google Ads. A função `urlDaP1()` do `presell.html` já faz isso (repassa todos os parâmetros da URL, como `gclid` e `utm_campaign`); é só tirar o painel de teste.
- **P1:** mude `mostrarDebug` para `false`. O que acontece depois da última pergunta fica no ponto marcado com `AQUI entra o próximo passo` (por enquanto só aparece uma mensagem de teste).
