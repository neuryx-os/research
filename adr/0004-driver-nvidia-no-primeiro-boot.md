# 0004 — Driver NVIDIA e CUDA instalados no primeiro boot

- **Status:** Proposto
- **Data:** 2026-10-28

> **Condição para aceite:** conclusão do tópico de pesquisa
> [01 — Licenciamento NVIDIA e CUDA](../topics/01-licenciamento-nvidia-cuda.md),
> confirmando o que pode e o que não pode ser redistribuído na imagem.

## Contexto

O Neuryx é otimizado para GPUs NVIDIA. O driver tem duas partes: o módulo de
kernel (disponível também como módulos abertos, `nvidia-open`) e o userspace
(bibliotecas como `libcuda`, `libnvidia-ml`). O CUDA Toolkit e o userspace do
driver são distribuídos sob EULAs da NVIDIA com restrições de redistribuição.
Além disso, gerações diferentes de GPU exigem ramos diferentes do driver.

O Lyra OS Desktop já segue o mesmo princípio: gera a ISO sem NVIDIA
pré-instalada e instala o driver depois, pelo Vega.

## Decisão

O driver NVIDIA e o CUDA **não fazem parte da ISO** nem dos pacotes do Neuryx.
Eles são instalados no **primeiro boot** pelo `neuryxctl` (`neuryxctl gpu
setup`), a partir do **repositório oficial da NVIDIA para openSUSE**, depois
de detectar a GPU presente.

## Justificativa

- Evita redistribuir componentes cuja EULA restringe a redistribuição.
- Permite escolher o ramo do driver adequado à GPU detectada, cobrindo várias
  gerações de hardware sem refazer a imagem.
- Mantém a imagem menor e independente do ciclo de releases da NVIDIA.

## Consequências

- O primeiro boot exige acesso à rede para usar a GPU; sem rede, o sistema
  funciona apenas com a variante CPU (ou Vulkan) do llama.cpp.
- O `neuryxctl` passa a ser responsável por detecção de GPU, adição do
  repositório NVIDIA, instalação e verificação do driver.
- Nenhum spec do `neuryx-packages` pode declarar o driver NVIDIA ou o CUDA
  como dependência; a variante CUDA do llama.cpp depende do runtime instalado
  pelo usuário.
- Se a pesquisa 01 mostrar que parte dos componentes pode ser redistribuída
  (por exemplo, módulos abertos), este ADR será revisto antes do aceite.

## Alternativas consideradas

- **Incluir driver e CUDA na ISO:** melhor experiência offline, mas com risco
  de violar a EULA e de envelhecer rápido. Rejeitada, sujeita à pesquisa 01.
- **Incluir apenas os módulos abertos (`nvidia-open`) na ISO:** possível
  meio-termo; depende da pesquisa 01 e de o userspace também ser instalável.
- **Delegar a instalação ao Vega:** o Vega já instala NVIDIA no Lyra, mas o
  Neuryx precisa do fluxo também em servidores headless e de forma scriptável;
  o `neuryxctl` pode reaproveitar os mesmos padrões.
