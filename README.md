# Reusable workflows

## Como usar:

### Workflow de labels

Adicione no seu workflow o seguinte trecho:

```yaml
  add-label:
    name: Adiciona labels
    uses: cebindani/reusable-workflows/.github/workflows/labeler.yml@main
    with:
      config-path: .github/labeler.yml
    secrets:
      repo-token: ${{ secrets.GITHUB_TOKEN }}
```

Para configurar as labels e regras, adicione na pasta `.github` o arquivo `labeler.yml`. Para mais informações, visite [actions/labeler](https://github.com/actions/labeler)

### Workflow de validação de pull-requests

```yaml
  pull-request-validator:
    name: Valida abertura do PR
    uses: cebindani/reusable-workflows/.github/workflows/pull-request-validator.yml@develop
    with:
      # Required labels do validate
      # Default values: "platform::android, platform::flutter, platform::iOS"
      platform-labels: "android, ios"

      # Default values: "scope::bug, scope::enhancements, scope::feature, scope::project, scope::question"
      scope-labels: "scope::bug, scope::feature"

      # Default values: "state::block, state::doing, state::done, state::ready_to_close, state::refining, state::review"
      state-labels: "state::block, state::doing, state::done"
    secrets:
      repo-token: ${{ secrets.GITHUB_TOKEN }}
```

Jobs disponíveis:
* Auto-assign do pull-request para o autor
* Validação do pull-request baseado no [Conventional Commits v1.0.0](https://www.conventionalcommits.org/en/v1.0.0/). Posta um comentário no pull request com exemplos.
* Validação de labels obrigatórias seguindo 3 pilares: plataforma, escopo e status. Os valores de `platform-labels`, `scope-labels` e `state-labels` são opcionais.
* Adiciona mensagem no final do template de pull request.

