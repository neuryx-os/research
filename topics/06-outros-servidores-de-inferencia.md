# 06 — Outros servidores de inferência

## Pergunta

Além do llama.cpp, quais servidores de inferência devem ser suportados?

## Por que importa

O llama.cpp atende bem a modelos GGUF em hardware variado, mas há casos de uso (alta concorrência, modelos não quantizados, ecossistema de ferramentas) em que outros servidores são mais adequados. Suportar mais servidores aumenta o custo de empacotamento e de manutenção.

## O que investigar

- vLLM: casos de uso (throughput, batching contínuo), dependências (Python, PyTorch, CUDA), viabilidade de empacotar como RPM.
- Ollama: casos de uso, relação com o llama.cpp, modelo de distribuição de modelos, licença e empacotamento.
- Custo de empacotamento e de atualização de cada um no OBS.
- Impacto nos ADRs [0004](../adr/0004-driver-nvidia-no-primeiro-boot.md) e [0007](../adr/0007-sem-gateway-e-monitoramento-proprios.md).

## Critério de conclusão

Existe uma recomendação escrita para cada servidor avaliado (suportar, documentar como opcional ou não suportar), com justificativa; recomendações de suporte geram um ADR.

## Fontes

<!-- Preencher durante a pesquisa. -->

## Conclusão

<!-- Preencher ao concluir. -->

## Status

Aberto
