# 0008 — Versionamento acompanha o Lyra

- **Status:** Aceito
- **Data:** 2026-10-28

## Contexto

O Neuryx é uma edição do Lyra OS Server
([ADR 0001](0001-edicao-do-lyra-server.md)), que por sua vez segue as versões
do openSUSE Leap (Lyra 16.1 sobre o Leap 16.1). O Neuryx precisa de um
esquema de versões antes do primeiro lançamento.

## Decisão

A versão do Neuryx **é a versão do Lyra OS sobre a qual ele é construído**. O
primeiro lançamento é o **Neuryx 16.1**, baseado no Lyra OS Server 16.1. Os
pré-lançamentos seguem a nomenclatura do Lyra: Alpha N, Beta, RC N.

## Justificativa

Como o Neuryx consome os pacotes e patterns do Lyra, a versão informa de
imediato qual base o usuário tem, quais pacotes recebe e até quando há
suporte. Uma numeração própria exigiria uma tabela de correspondência.

## Consequências

- Cada versão do Neuryx depende de uma versão estável do Lyra; o Neuryx 16.1
  pode sair depois do Lyra 16.1, mas nunca antes.
- A dependência é de mão única: o Lyra OS é um projeto separado, com
  cronograma próprio, e não ajusta suas datas ao Neuryx.
- O ciclo de vida do Neuryx acompanha o do Lyra.
- A versão do `neuryxctl` é independente e segue o próprio versionamento
  semântico; só a distribuição usa a versão do Lyra.
- O `neuryx-release` declara a mesma versão do Lyra em `/etc/os-release`.

## Alternativas consideradas

- **Numeração própria (Neuryx 1.0, 2.0...):** independente do Lyra, mas exige
  correspondência explícita com a base. Rejeitada.
- **Versionamento por data (por exemplo, 2027.04):** comum em distribuições
  contínuas, mas o Neuryx segue uma base de ciclo fixo. Rejeitada.
