# 05 — Suporte a AMD, Vulkan e CPU

## Pergunta

Como atender GPUs não NVIDIA e máquinas sem GPU?

## Por que importa

O Neuryx é otimizado para NVIDIA, mas parte dos usuários terá GPUs AMD ou Intel, ou nenhuma GPU. Além disso, o ADR 0004 faz o primeiro boot depender de rede para usar CUDA; as variantes CPU e Vulkan são o caminho sem driver proprietário.

## O que investigar

- Backends do llama.cpp: CPU (AVX2, AVX-512), Vulkan, ROCm/HIP, SYCL.
- Disponibilidade de ROCm e de drivers Vulkan (Mesa RADV, ANV) no openSUSE Leap 16.
- Desempenho relativo de Vulkan e ROCm em GPUs AMD, medido com `llama-bench`.
- Custo de manter cada variante (tempo de build no OBS, testes, suporte).

## Critério de conclusão

Existe uma lista das variantes suportadas oficialmente, com justificativa e custo estimado, e a regra de seleção automática da variante no `neuryxctl`.

## Fontes

<!-- Preencher durante a pesquisa. -->

## Conclusão

<!-- Preencher ao concluir. -->

## Status

Aberto
