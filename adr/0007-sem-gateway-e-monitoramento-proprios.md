# 0007 — Sem gateway nem monitoramento próprios no início

- **Status:** Aceito
- **Data:** 2026-10-28

## Contexto

Distribuições de inferência costumam oferecer um gateway de API (roteamento
entre modelos, autenticação, cotas) e um sistema de monitoramento. O
`llama-server` do llama.cpp já expõe uma API HTTP compatível com a da OpenAI, e
existem exportadores Prometheus mantidos pela comunidade para métricas de GPU
NVIDIA.

## Decisão

No início, o Neuryx **não cria gateway nem monitoramento próprios**. A API é a
do próprio `llama-server`; métricas de GPU usam **exportadores Prometheus
existentes**.

## Justificativa

Componentes próprios só se justificam quando houver uso real que mostre a
necessidade. Criar um gateway e um monitoramento antes disso aumentaria a
superfície de manutenção sem demanda comprovada.

## Consequências

- Cada modelo servido corresponde a uma instância do `llama-server`, gerida por
  unidades systemd criadas pelo `neuryxctl`.
- Autenticação, TLS e roteamento entre modelos, quando necessários, ficam a
  cargo de ferramentas existentes (por exemplo, um proxy reverso) e são
  documentados, não desenvolvidos.
- A escolha e o empacotamento de um exportador de métricas de GPU podem ser
  tratados em pesquisa futura.
- Esta decisão deve ser revista quando houver casos de uso concretos que não
  sejam atendidos.

## Alternativas consideradas

- **Gateway próprio desde o início:** antecipa necessidades não comprovadas.
  Rejeitada por ora.
- **Adotar um gateway de terceiros como parte da distribuição:** possível no
  futuro; depende de demanda e do tópico [06](../topics/06-outros-servidores-de-inferencia.md).
