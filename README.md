# Teste: presell + P1 com layout dinâmico

Várias presells mandam o visitante para a **mesma P1**. A P1 lê a `utm_source` da URL e mostra o layout daquela presell (Layout 1, 2 ou 3).

## Arquivos

| Arquivo | O que é |
|---|---|
| [`index.html`](index.html) | **Presell** de teste. É a página que abre na raiz do site: 2 perguntas e, no último passo, um painel (só de teste) para escolher qual `utm_source` mandar. |
| [`p1.html`](p1.html) | **P1**: URL única que troca o layout conforme a `utm_source` que chega. Sem `utm_source`, a página fica bloqueada com um alerta. |

As duas partes são HTML puro, cada uma em um arquivo só: o CSS e o script ficam dentro do próprio arquivo, sem nenhum arquivo externo.

## Links

- Presell: https://gabrielaacristofolini-hue.github.io/teste-layout-dinamico/
- P1: https://gabrielaacristofolini-hue.github.io/teste-layout-dinamico/p1.html?utm_source=source2

O GitHub Pages publica a branch **main**, pasta **/ (root)** (Settings → Pages).

## Como a P1 escolhe o layout

| `utm_source` | Layout |
|---|---|
| `source1` | Layout 1 (azul) |
| `source2` | Layout 2 (verde) |
| `source3` | Layout 3 (laranja) |
| desconhecida (ex.: `google`) | Layout 1 (padrão) |
| sem `utm_source` | página bloqueada: fundo preto borrado e um alerta pedindo a source |

Maiúsculas não importam (`Source2` = `source2`). Essa tabela fica no `CONFIG`, no fim do `p1.html`. O bloqueio liga e desliga em `bloquearSemSource`.

## Adicionar uma operação nova (ex.: Layout 4)

1. No `p1.html`, copie um bloco `<template id="layout-3"> … </template>`, troque para `id="layout-4"` e `class="layout layout-4"`, e edite o HTML como quiser.
2. No CSS do `p1.html`, crie as cores: `.layout-4 { --cor: …; --cor-escura: …; --fundo: …; }`.
3. No `CONFIG.layoutPorSource`, adicione `minhasource: 'layout-4'`.
4. Na campanha do Google Ads, use no **sufixo do URL final**: `utm_source=minhasource`.

## Levando para a operação

- **Presells reais:** o painel de escolher a `utm_source` não existe no funil. Nas presells reais a `utm_source` vem da campanha do Google Ads, e o botão final só repassa a URL que chegou para a P1. A função `urlDaP1()` do `index.html` já faz isso (leva junto `gclid`, `utm_campaign` etc.).
- **P1:** mude `mostrarDebug` para `false`. O que acontece depois da última pergunta fica no ponto marcado com `AQUI entra o próximo passo` (por enquanto só aparece uma mensagem de teste).
