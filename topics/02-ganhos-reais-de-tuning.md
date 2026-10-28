# 02 — Ganhos reais de tuning

## Pergunta

Quais ajustes do sistema trazem ganho mensurável na inferência?

## Por que importa

O repositório [`neuryx-tuning`](https://github.com/neuryx-os/neuryx-tuning) só deve conter ajustes com ganho comprovado. Ajustes sem medição podem não ter efeito, piorar outras cargas ou mascarar problemas.

## O que investigar

- Governor de CPU e `energy_perf_bias` (perfis do `tuned`).
- Hugepages (transparentes e estáticas) e `vm.nr_hugepages`.
- `memlock` ilimitado para permitir `--mlock` no llama.cpp.
- NUMA pinning em máquinas com mais de um socket.
- Persistence mode da GPU NVIDIA.
- Swap e `vm.swappiness`.
- Antes de adotar qualquer valor: definir um benchmark reproduzível com `llama-bench` (modelos, quantizações, tamanhos de prompt e de geração, número de repetições, hardware de referência).

## Critério de conclusão

Existe um procedimento de benchmark documentado em `neuryx-tuning/bench/` e, para cada ajuste candidato, uma medição antes e depois em pelo menos um hardware de referência; os ajustes com ganho consistente são promovidos e os demais descartados.

## Fontes

<!-- Preencher durante a pesquisa. -->

## Conclusão

<!-- Preencher ao concluir. -->

## Status

Aberto
