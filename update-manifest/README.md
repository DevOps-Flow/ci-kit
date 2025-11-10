# update-manifest

Atualiza o campo `image:` em um **Deployment** Kubernetes via `yq`, valida e faz **commit/push** da alteração (GitOps).

## Quando usar
- Antes do deploy via Argo CD, para apontar o manifest para a nova imagem.

## Inputs
| Nome             | Obrigatório | Default                          | Descrição                             |
|------------------|-------------|----------------------------------|---------------------------------------|
| `file`           | não         | `k8s/20-deployment-service.yaml` | Caminho do YAML a alterar.            |
| `deploy_name`    | não         | `customer-api`                   | Nome do Deployment.                   |
| `container_name` | não         | `customer-api`                   | Nome do container dentro do Pod.      |
| `image_tag`      | sim         | —                                | `repo/image:tag` final.               |

## Outputs
Nenhum.

## Exemplo de uso
```yaml
- uses: lab-safer/ci-kit/update-manifest@v1
  with:
    file: k8s/20-deployment-service.yaml
    deploy_name: customer-api
    container_name: customer-api
    image_tag: ${{ needs.meta.outputs.IMAGE }}:${{ needs.meta.outputs.VERSION }}
```
## Requisitos

- Permissão de contents: write para commitar/push.

- Caminho do arquivo e nomes (deploy/container) corretos.

## Erros comuns

- imagem vazia após yq → confirme image_tag e seletor correto do Deployment/Container.

- Conflito de merge → o step já faz fetch/pull --rebase antes do push.

## Versionamento

- Tags semânticas: v1, v1.0.0
