# resolve-image

Resolve o nome final da imagem Docker com **fallback robusto**:
1) Usa `docker_image` se fornecido;
2) Senão, monta `<dockerhub_user>/<repo_name>`.

Valida o formato para evitar tags inválidas (ex.: `:1.0.0` sem repositório).

## Quando usar
- Antes do build/push de imagem para garantir que o nome está correto.

## Inputs
| Nome            | Obrigatório | Descrição                                     |
|-----------------|-------------|-----------------------------------------------|
| `docker_image`  | não         | Nome completo da imagem (ex.: `user/app`).    |
| `dockerhub_user`| não         | Usuário do Docker Hub (para fallback).        |
| `repo_name`     | sim         | Nome do repositório atual (ex.: `minha-api`). |

## Outputs
| Nome    | Descrição                 |
|---------|---------------------------|
| `image` | Nome final da imagem.     |

## Exemplo de uso
```yaml
- id: img
  uses: lab-safer/ci-kit/resolve-image@v1
  with:
    docker_image: ${{ vars.DOCKER_IMAGE }}
    dockerhub_user: ${{ secrets.DOCKERHUB_USERNAME }}
    repo_name: ${{ github.event.repository.name }}

# depois:
# ${{ steps.img.outputs.image }}
```
## Erros comuns

- dockerhub_user ausente e docker_image vazio → informe pelo menos um dos dois.

- Formato inválido: use apenas minúsculas, números, . _ - (ex.: user/minha-api).

## Versionamento

- Tags semânticas: v1, v1.1.0