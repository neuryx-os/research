# 0006 — Gestão gráfica via módulo de IA do Vega

- **Status:** Aceito
- **Data:** 2026-10-28

## Contexto

Usuários podem querer uma interface visual para acompanhar a GPU, os modelos
instalados e os serviços de inferência. O ecossistema Lyra já tem o Vega, centro
de controle com daemon (`vegad`), contrato D-Bus e frontends GTK, terminal e
web (`vega-web`), usado também no Lyra OS Server.

## Decisão

O Neuryx **não terá painel gráfico próprio**. A gestão visual de GPU e modelos
será um **módulo de IA do Vega**, mantido no ecossistema Lyra.

## Justificativa

Um painel próprio seria mais uma interface para manter, com autenticação,
segurança e testes próprios. Como módulo do Vega, a funcionalidade aproveita a
infraestrutura existente e passa a servir também ao Lyra OS.

## Consequências

- O módulo de IA do Vega precisa ser proposto e implementado na organização
  `lyra-os-linux`, fora do escopo deste repositório.
- O `neuryxctl` deve expor operações de forma que o Vega possa reutilizá-las
  (saída estruturada, códigos de saída estáveis) ou que a lógica possa migrar
  para o `vegad`.
- Até o módulo existir, a gestão é feita pela linha de comando.

## Alternativas consideradas

- **Painel web próprio do Neuryx:** duplicaria o `vega-web`. Rejeitada.
- **Usar interfaces de terceiros (por exemplo, a interface web embutida do
  `llama-server`):** úteis para conversar com o modelo, mas não cobrem gestão
  de GPU e serviços. Podem ser documentadas como complemento.
