# 04 — Dependência da base Lyra

## Pergunta

Qual o impacto da base do Lyra Server no Neuryx?

## Por que importa

O ADR [0001](../adr/0001-edicao-do-lyra-server.md) faz do Neuryx uma edição do Lyra OS Server. Tudo o que muda na base do Lyra afeta o Neuryx, e o `config.kiwi` do [`neuryx-server`](https://github.com/neuryx-os/neuryx-server) depende de existir no Lyra um pattern reutilizável do Server.

## O que investigar

- Estabilidade e ciclo de vida do openSUSE Leap 16 (e 16.1) para o caso de uso de inferência: versões de kernel, compiladores e Mesa/Vulkan.
- Eventual migração do Lyra para Debian e o que isso significaria para o Neuryx (KIWI, OBS, RPM).
- O que precisa existir no Lyra como pattern (nome, conteúdo, repositório OBS) para o ADR 0001 funcionar sem copiar a descrição KIWI do `lyraos-server`.
- Como o Neuryx deve ser registrado no catálogo `lyra-ecosystem` (`products.toml`, relações `consumes`).

## Critério de conclusão

Existe uma especificação do pattern do Lyra Server necessário (pacotes e nome), acordada com o projeto Lyra, e uma avaliação escrita dos riscos de base com plano para cada um.

## Fontes

<!-- Preencher durante a pesquisa. -->

## Conclusão

<!-- Preencher ao concluir. -->

## Status

Aberto
