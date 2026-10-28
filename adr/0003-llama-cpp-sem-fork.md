# 0003 — llama.cpp sem fork

- **Status:** Aceito
- **Data:** 2026-10-28

## Contexto

O [llama.cpp](https://github.com/ggml-org/llama.cpp) é o motor de inferência
principal do Neuryx. O projeto publica builds quase diariamente, com mudanças
frequentes de flags de compilação, backends e formato de modelos. O Neuryx
precisa entregar uma versão estável, compilada para diferentes backends.

## Decisão

O llama.cpp **não é bifurcado**. O pacote `llama-cpp`, mantido em
[`neuryx-packages`](https://github.com/neuryx-os/neuryx-packages), compila o
código upstream em uma **versão fixada e testada**, gerando as variantes
**CPU**, **CUDA** e **Vulkan** como subpacotes.

Patches locais, quando inevitáveis, ficam no próprio pacote, são mínimos e
devem ser enviados ao upstream.

## Justificativa

Com a cadência de releases do llama.cpp, um fork viraria um segundo projeto a
manter, com rebase constante e risco de ficar para trás em suporte a modelos.
Fixar uma versão testada dá previsibilidade sem esse custo.

## Consequências

- Atualizar o llama.cpp é uma decisão explícita: troca da versão no spec,
  build no OBS e testes antes de publicar.
- A política de atualização (quando e com que testes) é definida no tópico
  [03](../topics/03-versoes-do-llama-cpp.md).
- A variante CUDA é compilada contra o CUDA Toolkit no OBS, mas o runtime
  NVIDIA não é distribuído pelo Neuryx (ver ADR 0004).

## Alternativas consideradas

- **Manter um fork:** controle total, mas custo de manutenção desproporcional
  para a equipe. Rejeitada.
- **Acompanhar o upstream continuamente (sem fixar versão):** sempre atual,
  mas sem garantia de estabilidade. Rejeitada para o repositório principal;
  pode existir como canal de testes.
- **Usar binários pré-compilados do upstream:** não se integra ao OBS nem ao
  controle de dependências do RPM. Rejeitada.
