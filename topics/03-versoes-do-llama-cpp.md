# 03 — Versões do llama.cpp

## Pergunta

Fixar versões testadas ou acompanhar o upstream do llama.cpp?

## Por que importa

O ADR [0003](../adr/0003-llama-cpp-sem-fork.md) decide não bifurcar o llama.cpp e fixar uma versão testada, mas não define com que frequência atualizar nem quais testes exigir. O llama.cpp publica builds quase diariamente.

## O que investigar

- Cadência de releases e esquema de versionamento (tags `bNNNN`).
- Quebras de compatibilidade: formato GGUF, API do `llama-server`, ABI das bibliotecas, compatibilidade com versões do driver NVIDIA e do kernel.
- Variantes de build (CPU, CUDA, Vulkan) e flags relevantes (`GGML_CUDA`, `GGML_VULKAN`, `GGML_NATIVE`, arquiteturas CUDA alvo).
- Como outras distribuições empacotam o llama.cpp (openSUSE, Fedora, Arch, Debian).
- Viabilidade de um canal de testes acompanhando o upstream.

## Critério de conclusão

Existe uma política escrita de atualização (frequência, critérios, testes mínimos) e a lista de flags de build por variante, prontas para o spec do `llama-cpp`.

## Fontes

<!-- Preencher durante a pesquisa. -->

## Conclusão

<!-- Preencher ao concluir. -->

## Status

Aberto
