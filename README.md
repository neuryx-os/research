# research

Pesquisas técnicas e registros de decisão (ADRs) do Neuryx.

**Status:** Em pesquisa

## Propósito

Este repositório concentra o raciocínio por trás do Neuryx:

- **ADRs** (`adr/`): decisões de arquitetura, com contexto, justificativa,
  consequências e alternativas. Uma decisão com status *Aceito* só muda por
  meio de um novo ADR que a substitua.
- **Tópicos de pesquisa** (`topics/`): perguntas técnicas em aberto. Cada
  tópico tem uma issue correspondente com o label `tipo: pesquisa` e termina
  com uma conclusão que pode originar ou confirmar um ADR.

Nada aqui é compilado ou empacotado.

O plano e o cronograma do projeto estão em [`ROADMAP.md`](ROADMAP.md).

## Estrutura

```
research/
├── ROADMAP.md     # plano e cronograma
├── adr/
│   ├── README.md      # índice dos ADRs
│   ├── template.md    # modelo para novos ADRs
│   └── NNNN-*.md
└── topics/
    ├── README.md      # índice dos tópicos
    └── NN-*.md
```

## Como contribuir

- **Novo ADR:** copie `adr/template.md` para `adr/NNNN-titulo-curto.md` com o
  próximo número livre, preencha e adicione ao índice `adr/README.md`. Abra o
  pull request com o label `tipo: decisão`.
- **Novo tópico:** crie `topics/NN-titulo-curto.md` seguindo o formato dos
  existentes, adicione ao índice e abra uma issue com o label `tipo: pesquisa`.
- **Concluir um tópico:** preencha *Fontes* e *Conclusão*, mude o status para
  `Concluído` e referencie o ADR afetado, se houver.

## Relação com outros repositórios

Os ADRs orientam todos os repositórios da organização:

- [`neuryx-server`](https://github.com/neuryx-os/neuryx-server): ADR 0001, tópico 04.
- [`neuryx-packages`](https://github.com/neuryx-os/neuryx-packages): ADRs 0001, 0003 e 0004, tópicos 01 e 03.
- [`neuryx-tuning`](https://github.com/neuryx-os/neuryx-tuning): tópico 02.
- [`neuryxctl`](https://github.com/neuryx-os/neuryxctl): ADRs 0004, 0005 e 0007.
- [`.github`](https://github.com/neuryx-os/.github): ADR 0002 (convenções).

## Licença

O conteúdo deste repositório está licenciado sob a
[Creative Commons Atribuição-CompartilhaIgual 4.0 Internacional (CC BY-SA 4.0)](LICENSE).
