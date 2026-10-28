# 0005 — `neuryxctl` em Go

- **Status:** Aceito
- **Data:** 2026-10-28

## Contexto

O Neuryx precisa de uma ferramenta de linha de comando para configurar a GPU,
baixar e verificar modelos e gerenciar os serviços de inferência. Ela conversa
com o systemd e o D-Bus, roda em servidores headless e precisa ser simples de
empacotar.

## Decisão

O `neuryxctl` é escrito em **Go**.

## Justificativa

- É o mesmo stack do `vegad`, o daemon do Vega no ecossistema Lyra, o que
  permite reaproveitar padrões de código, de empacotamento e de integração com
  systemd e D-Bus.
- Go gera binário estático, sem dependências de runtime, adequado a uma
  ferramenta de sistema.
- A biblioteca padrão cobre HTTP, hashing, JSON e execução de processos,
  necessários para baixar e verificar modelos.

## Consequências

- O pacote RPM do `neuryxctl` é construído no OBS com o toolchain Go do
  openSUSE.
- Dependências externas devem ser poucas e justificadas; o esqueleto inicial
  usa apenas a biblioteca padrão.
- A CI do repositório roda `go vet`, `go test` e `go build`.

## Alternativas consideradas

- **Rust:** usado em outros componentes do Lyra, mas o paralelo mais direto
  (daemon de sistema com systemd e D-Bus) é o `vegad`, em Go. Rejeitada.
- **Python:** rápido para prototipar, mas depende de runtime e de bibliotecas
  no sistema. Rejeitada.
- **Bash:** suficiente para scripts pequenos, mas não escala para gestão de
  modelos e verificação de integridade. Rejeitada.
