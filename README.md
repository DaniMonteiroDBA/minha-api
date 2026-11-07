# Contratos e governança de APIs

Laboratório de API First para uma API de gestão de clientes. O repositório reúne um contrato OpenAPI 3.0.3, regras Spectral e documentação gerada com Redoc.

O foco é tornar decisões de interface e governança inspecionáveis antes da implementação: operações, formatos de resposta, autenticação declarada e requisitos de acesso.

## Escopo

O contrato descreve cadastro, consulta, atualização e remoção de clientes. Também declara autenticação Bearer, requisitos de escopo por operação e respostas com dados parcialmente mascarados.

Essas definições são requisitos do contrato. O repositório não contém o servidor da API, e sua presença no OpenAPI não comprova que autenticação, autorização ou mascaramento foram implementados. Os endereços de servidor são exemplos.

## Arquivos principais

| Arquivo | Finalidade |
| --- | --- |
| [openapi.yaml](openapi.yaml) | Contrato da API de gestão de clientes. |
| [spectral-gestao-clientes.yaml](spectral-gestao-clientes.yaml) | Regras Spectral específicas para o contrato de clientes. |
| [spectral.yaml](spectral.yaml) | Outro conjunto de regras disponível no acervo; selecione o ruleset explicitamente ao executar o lint. |
| [docs/index.html](docs/index.html) | Documentação HTML gerada. |
| [.github/workflows/ci-cd.yml](.github/workflows/ci-cd.yml) | Workflow que gera a documentação e a publica na branch de GitHub Pages. |

## Explorar o contrato

1. Leia `info`, `servers`, `paths` e `components` em `openapi.yaml`.
2. Compare uma operação com as regras em `spectral-gestao-clientes.yaml`.
3. Observe como os requisitos de leitura e escrita são declarados em `x-required-scope`.
4. Compare respostas de sucesso e erro e registre as decisões que uma implementação precisaria cumprir.

## Executar as ferramentas

É necessário ter Node.js e npm disponíveis. Os comandos abaixo usam `npx`, que pode baixar os pacotes necessários. Eles reproduzem as ferramentas declaradas no repositório; não há versão fixada ou compatibilidade de runtime documentada atualmente.

Para executar o lint com o conjunto específico de regras:

```sh
npx @stoplight/spectral-cli lint openapi.yaml --ruleset spectral-gestao-clientes.yaml
```

Para gerar novamente a documentação:

```sh
npx --yes @redocly/cli build-docs openapi.yaml --output docs/index.html
```

## Validação e evolução

O workflow atual gera e publica documentação em pushes na branch `main` e por acionamento manual. Ele não contém um job de validação Spectral, apesar de um comentário mencionar essa etapa.

Os próximos passos para transformar o laboratório em uma referência reproduzível são fixar as versões das ferramentas, registrar uma execução real do lint, resolver os achados e incluir a validação como condição para publicar a documentação. A implementação e os testes de integração da API são uma etapa separada.

## Autoria

[Dani Monteiro](https://danimonteiro.tech) — engenharia de dados e IA, arquitetura, pesquisa e educação.
