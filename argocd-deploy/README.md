# argocd-deploy

Executa **Argo CD sync + wait**. Em caso de falha, faz **rollback GitOps** (reverte o último commit) e sincroniza novamente.

## Quando usar
- No final do pipeline, para implantar via Argo CD e garantir saúde do app.

## Inputs
| Nome                   | Obrigatório | Default   | Descrição                                 |
|------------------------|-------------|-----------|-------------------------------------------|
| `server`               | sim         | —         | URL/host do Argo CD (ex.: `argocd.example.com`). |
| `token`                | sim         | —         | Token de autenticação do Argo CD.         |
| `app`                  | sim         | —         | Nome do `Application` do Argo CD.         |
| `cli_version`          | não         | `v2.13.3` | Versão do container CLI do Argo CD.       |
| `cli_version_rollback` | não         | `v2.12.3` | Versão usada no rollback.                  |

## Outputs
Nenhum.

## Exemplo de uso
```yaml
- uses: lab-safer/ci-kit/argocd-deploy@v1
  with:
    server: ${{ secrets.ARGOCD_SERVER }}
    token:  ${{ secrets.ARGOCD_TOKEN }}
    app:    ${{ secrets.ARGOCD_APP }}
```
## Requisitos

- ARGOCD_SERVER, ARGOCD_TOKEN, ARGOCD_APP válidos.

- Histórico Git consistente (rollback usa git revert HEAD).

## Erros comuns

- Permissão negada no Argo → confira token/role.

- Rollback falhou por histórico “sujo” → valide commits recentes no branch.

## Versionamento

- Tags semânticas: v1, v1.0.0