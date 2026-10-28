# 0002 — Organização e convenções

- **Status:** Aceito
- **Data:** 2026-10-28

## Contexto

O Neuryx precisa de um lugar próprio no GitHub e de convenções de nomes,
branches e commits. O ecossistema Lyra já tem um padrão na organização
`lyra-os-linux`: repositórios de produto com prefixo (`lyraos-*`) e
repositórios institucionais ou de produtos independentes sem prefixo (`site`,
`vega`).

## Decisão

- Organização: [`neuryx-os`](https://github.com/neuryx-os).
- Repositórios de produto com prefixo `neuryx-` (por exemplo, `neuryx-server`,
  `neuryx-packages`, `neuryx-tuning`). A CLI chama-se `neuryxctl`, que já
  carrega o nome do projeto.
- Repositórios institucionais sem prefixo: `.github`, `research`, `brand`,
  `site`.
- Branch padrão: `main`.
- Commits no padrão [Conventional Commits](https://www.conventionalcommits.org/pt-br/v1.0.0/),
  com descrição em português.
- Integração de pull requests apenas por squash, com exclusão automática da
  branch.

## Justificativa

Seguir o padrão já usado no Lyra reduz o custo de alternar entre os dois
projetos e facilita a automação comum. Conventional Commits permite gerar
changelogs e identificar mudanças incompatíveis; o squash mantém um histórico
linear com um commit por mudança.

## Consequências

- Novos repositórios de produto devem seguir o prefixo `neuryx-`.
- O título de cada pull request precisa seguir Conventional Commits, porque
  vira a mensagem do commit de squash.
- Os labels padronizados (`tipo:`, `prioridade:`, `status:`) são os mesmos em
  todos os repositórios de código e pesquisa.

## Alternativas consideradas

- **Repositórios dentro de `lyra-os-linux`:** misturaria dois produtos com
  públicos e ciclos diferentes na mesma organização. Rejeitada.
- **Monorepo único para o Neuryx:** simplifica o início, mas mistura licenças
  (CC BY-SA, GPL, marca) e fluxos de build diferentes (KIWI, OBS, Go). Rejeitada.
- **Commits em inglês:** o restante do ecossistema Lyra usa português. Rejeitada.
