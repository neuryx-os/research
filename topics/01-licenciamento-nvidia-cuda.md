# 01 — Licenciamento NVIDIA e CUDA

## Pergunta

O que pode ser redistribuído na ISO entre driver NVIDIA, módulos abertos (`nvidia-open`) e CUDA?

## Por que importa

O ADR [0004](../adr/0004-driver-nvidia-no-primeiro-boot.md) propõe deixar driver e CUDA fora da ISO e instalá-los no primeiro boot. Ele só pode ser aceito depois de sabermos com segurança o que a NVIDIA permite redistribuir. A resposta também define se a variante CUDA do `llama-cpp` pode ser publicada no OBS e com quais dependências.

## O que investigar

- EULA do driver NVIDIA para Linux (userspace) e licença dos módulos de kernel abertos (`nvidia-open`).
- EULA do CUDA Toolkit e o anexo com a lista de bibliotecas de runtime redistribuíveis (por exemplo, `cudart`, `cublas`).
- Se um binário compilado contra CUDA (como a variante CUDA do `llama-cpp`) pode ser distribuído e com quais bibliotecas.
- Como o openSUSE resolve isso (repositório da NVIDIA, pacotes `nvidia-open-driver-G06-signed`, Secure Boot).
- Como outras distribuições resolvem isso (por exemplo, Ubuntu, Fedora/RPM Fusion, Pop!_OS).

## Critério de conclusão

Existe uma tabela, com fonte para cada linha, dizendo para driver userspace, módulos abertos, CUDA Toolkit e bibliotecas de runtime se podem ou não ir na ISO e nos repositórios do Neuryx; e o ADR 0004 foi aceito, ajustado ou rejeitado com base nela.

## Fontes

<!-- Preencher durante a pesquisa. -->

## Conclusão

<!-- Preencher ao concluir. -->

## Status

Aberto
