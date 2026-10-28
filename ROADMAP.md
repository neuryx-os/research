# Roadmap do Neuryx

Plano e cronograma do primeiro lançamento, o **Neuryx 16.1**, baseado no Lyra
OS Server 16.1 (openSUSE Leap 16.1). A numeração acompanha o Lyra
([ADR 0008](adr/0008-versionamento-acompanha-o-lyra.md)).

- **Atualizado em:** 2026-10-28
- **Início:** depois do lançamento do Lyra OS 16.1 (previsto pelo Lyra para até 26/11/2026)
- **Alvo do Neuryx 16.1:** maio de 2027

## Premissas

- **O Lyra OS e o Neuryx são projetos separados.** O Lyra tem cronograma
  próprio e não se ajusta às datas do Neuryx. Este roadmap só agenda trabalho
  do Neuryx; o que depende do Lyra aparece como
  [dependência externa](#dependências-externas-lyra-os), sem data.
- **O trabalho no Neuryx só começa depois do lançamento do Lyra OS 16.1.**
  Até lá, o foco é o Lyra. As datas abaixo supõem o lançamento até
  26/11/2026; se ele mudar, a Fase 0 começa logo após o lançamento e as
  demais fases andam junto.
- Um mantenedor em tempo parcial.
- Os marcos valem mais que as datas. Cada fase termina num estado que
  funciona; se uma dependência ou o tempo faltar, as datas do Neuryx mudam e
  os marcos permanecem.

## Caminho crítico

```
[Lyra] pattern do Lyra Server ──► config.kiwi ──► primeira imagem
tópico 01 (licenças) ───────────► ADR 0004 ─────► variante CUDA + gpu setup
```

O restante pode avançar em paralelo.

## Visão geral

| Fase | Período | Marco |
| --- | --- | --- |
| 0 — Pesquisa | Dezembro de 2026 | ADR 0004 decidido e pattern do Lyra Server especificado |
| 1 — Pacotes | Janeiro de 2027 | Pacotes do Neuryx compilando no OBS |
| 2 — Primeira imagem | Fevereiro de 2027 | **Neuryx 16.1 Alpha 1** (qcow2) |
| 3 — Serviço e ajustes | Março de 2027 | **Neuryx 16.1 Alpha 2** (ISO e qcow2) |
| 4 — Estabilização | Abril de 2027 | **Neuryx 16.1 Beta**, com congelamento de funcionalidades |
| 5 — Lançamento | Maio de 2027 | **Neuryx 16.1** |

## Dependências externas (Lyra OS)

Itens que pertencem ao Lyra OS e seguem o cronograma do Lyra. O Neuryx pode
propô-los e especificá-los, mas não define quando acontecem.

| Dependência | Necessária para | Situação |
| --- | --- | --- |
| Lyra OS Server 16.1 estável | Fase 2 em diante e lançamento | Em andamento no Lyra |
| Pattern reutilizável do Lyra Server publicado no OBS ([ADR 0001](adr/0001-edicao-do-lyra-server.md)) | Fase 2 (imagem) | Especificação na Fase 0 do Neuryx |
| Registro do Neuryx no catálogo `lyra-ecosystem` | Coerência entre os projetos | A propor ao Lyra |
| Módulo de IA do Vega ([ADR 0006](adr/0006-gestao-grafica-via-vega.md)) | Gestão gráfica (após o 16.1) | A propor ao Lyra |

Se uma dependência não estiver pronta quando a fase do Neuryx que precisa dela
começar, a fase espera e o cronograma do Neuryx é atualizado aqui.

## Fase 0 — Pesquisa (dezembro de 2026)

Começa depois do lançamento do Lyra OS 16.1.

- [ ] Concluir o [tópico 01](topics/01-licenciamento-nvidia-cuda.md) e aceitar ou revisar o [ADR 0004](adr/0004-driver-nvidia-no-primeiro-boot.md).
- [ ] Concluir o [tópico 03](topics/03-versoes-do-llama-cpp.md): política de versões e flags de build do llama.cpp.
- [ ] [Tópico 04](topics/04-dependencia-da-base-lyra.md): especificar o pattern do Lyra Server de que o Neuryx precisa e propô-lo ao projeto Lyra.
- [ ] `neuryxctl gpu detect`, somente leitura.
- [ ] Escolher a hospedagem do site e apontar o domínio `neuryx-os.com.br`.

**Marco:** ADR 0004 com status final e proposta do pattern entregue ao Lyra.

## Fase 1 — Pacotes (janeiro de 2027)

- [ ] Criar o projeto OBS `home:rodrigosbrito:lyra:Neuryx`.
- [ ] `llama-cpp` compilando no OBS nas variantes CPU e Vulkan.
- [ ] Empacotar `neuryx-release`, `patterns-neuryx` e `neuryxctl`.

**Marco:** pacotes do Neuryx compilando no OBS. A instalação de
`patterns-neuryx` sobre um Lyra Server depende do pattern do Lyra estar
publicado.

## Fase 2 — Primeira imagem (fevereiro de 2027)

Requer: pattern do Lyra Server publicado e Lyra OS Server 16.1 estável.

- [ ] `config.kiwi` do `neuryx-server` com o perfil qcow2.
- [ ] `neuryxctl gpu setup` instalando o driver a partir do repositório oficial da NVIDIA.
- [ ] Variante CUDA do `llama-cpp`, na forma permitida pelo tópico 01.
- [ ] `neuryxctl model pull`, `model list` e `model verify`.

**Marco — Neuryx 16.1 Alpha 1:** imagem qcow2 que inicializa, instala o driver
no primeiro boot e roda um modelo na CPU e na GPU.

## Fase 3 — Serviço e ajustes (março de 2027)

- [ ] `neuryxctl serve enable` e `serve status`, com unidades systemd do `llama-server`.
- [ ] [Tópico 02](topics/02-ganhos-reais-de-tuning.md): benchmark com `llama-bench`; adotar no `neuryx-tuning` só os ajustes com ganho medido.
- [ ] ISO de instalação.

**Marco — Neuryx 16.1 Alpha 2:** ISO e qcow2, com modelo servido pela API
compatível com OpenAI.

## Fase 4 — Estabilização (abril de 2027)

- [ ] Testes em hardware real, com pelo menos uma GPU NVIDIA de referência.
- [ ] Documentação de instalação e uso; atualizar o site.
- [ ] Imagem de nuvem com `cloud-init`.

**Marco — Neuryx 16.1 Beta:** congelamento de funcionalidades; a partir daqui,
apenas correções.

## Fase 5 — Lançamento (maio de 2027)

- [ ] Candidata de lançamento (RC) e correções.
- [ ] Lançamento do **Neuryx 16.1**.

## Depois do 16.1

- [Tópico 05](topics/05-suporte-amd-vulkan-cpu.md): AMD (ROCm) e outras GPUs.
- [Tópico 06](topics/06-outros-servidores-de-inferencia.md): vLLM e Ollama.
- Neuryx 16.2, quando houver Lyra OS Server 16.2.

## Riscos

| Risco | Efeito | Mitigação |
| --- | --- | --- |
| Pattern do Lyra Server não estar publicado no início da Fase 2 | Fase 2 e seguintes atrasam | Entregar a especificação cedo (Fase 0); adiantar trabalho da Fase 3 que não depende da imagem |
| Tópico 01 impedir distribuir a variante CUDA | CUDA compilada pelo usuário ou suporte só via Vulkan | Decidir ainda na Fase 0 |
| Pouco tempo do mantenedor | Todas as datas | Marcos acima das datas; cada fase termina num estado que funciona |
