# 0001 — Neuryx como edição do Lyra OS Server

- **Status:** Aceito
- **Data:** 2026-10-28

## Contexto

O Neuryx é uma distribuição voltada à inferência de modelos de IA locais. Ele
precisa de uma base de servidor estável: instalador, kernel, rede, firewall,
atualizações e ferramentas de administração. O Lyra OS Server
([`lyra-os-linux/lyraos-server`](https://github.com/lyra-os-linux/lyraos-server)),
baseado no openSUSE Leap 16, já resolve tudo isso, com imagens geradas por KIWI
e pacotes publicados no OBS.

A equipe é pequena e mantém as duas distribuições. Qualquer duplicação entre
elas vira trabalho repetido a cada correção.

## Decisão

O Neuryx é uma **edição do Lyra OS Server**. A base vem dos **pacotes e
patterns do Lyra**, consumidos do repositório OBS do Lyra. O Neuryx adiciona
apenas a camada de IA, reunida no pattern `patterns-neuryx`.

A descrição KIWI do `lyraos-server` **nunca é copiada** para o Neuryx. A
descrição KIWI do Neuryx (`neuryx-server`) referencia o pattern do Lyra Server
e acrescenta o pattern do Neuryx.

## Justificativa

Uma cópia da descrição KIWI começaria idêntica e divergiria a cada mudança no
Lyra, exigindo sincronização manual. Consumindo pacotes e patterns, cada
correção publicada pelo Lyra chega ao Neuryx automaticamente no próximo build
da imagem. Isso torna viável manter as duas distribuições com uma equipe
pequena.

## Consequências

- É pré-requisito existir, no Lyra, um **pattern reutilizável do Server** que
  descreva o conjunto de pacotes da edição. Enquanto ele não existir, o
  `neuryx-server` não tem `config.kiwi` funcional.
- O Neuryx herda o ciclo de vida, a estabilidade e as decisões de base do
  Lyra (ver tópico [04](../topics/04-dependencia-da-base-lyra.md)).
- Mudanças necessárias na base devem ser feitas no Lyra, não contornadas no
  Neuryx.
- O overlay de arquivos do Neuryx (`neuryx-server/root/`) deve se limitar ao
  que é específico da IA.

## Alternativas consideradas

- **Copiar a descrição KIWI do `lyraos-server` e adaptá-la:** rápido no
  início, mas cria divergência permanente e dobra a manutenção. Rejeitada.
- **Distribuição independente sobre o openSUSE Leap:** repetiria todo o
  trabalho de base já feito no Lyra. Rejeitada.
- **Apenas um repositório de pacotes instalável sobre o Lyra Server, sem
  imagem própria:** possível como complemento, mas não oferece imagem pronta
  para instalação e nuvem. Não descartada como forma adicional de distribuição.
