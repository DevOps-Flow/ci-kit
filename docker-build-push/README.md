# docker-build-push

Faz **build** e **push** da imagem Docker com **Buildx** e **cache remoto** no registry (Docker Hub). Publica as tags `:VERSION` e `:latest`.

## Quando usar
- Para montar a imagem final do serviço e publicar no Docker Hub.
- Para acelerar builds com cache persistente entre runners efêmeros.

## Inputs
| Nome             | Obrigatório | Descrição                                      |
|------------------|-------------|------------------------------------------------|
| `image`          | sim         | Nome completo da imagem (ex.: `user/app`).     |
| `version`        | sim         | Versão (ex.: `1.0.10`).                        |
| `dockerfile`     | sim         | Caminho do Dockerfile (ex.: `./Dockerfile.native`). |
| `context`        | sim         | Contexto do build (ex.: `.`).                  |
| `dockerhub_user` | sim         | Usuário do Docker Hub (para login).            |
| `dockerhub_token`| sim         | Token/senha do Docker Hub (para login).        |

## Outputs
Nenhum.

## Exemplo de uso
```yaml
- uses: lab-safer/ci-kit/docker-build-push@v1
  with:
    image: ${{ steps.img.outputs.image }}
    version: ${{ needs.meta.outputs.VERSION }}
    dockerfile: ./Dockerfile.native
    context: .
    dockerhub_user: ${{ secrets.DOCKERHUB_USERNAME }}
    dockerhub_token: ${{ secrets.DOCKERHUB_TOKEN }}
```
## Requisitos

- resolve-image antes (ou defina image diretamente).

- Artifact do binário nativo disponível no contexto (se o Dockerfile o copia).

## Erros comuns

- invalid reference format → verifique o image (não pode estar vazio).

- Falha de autenticação → confirme DOCKERHUB_USERNAME/DOCKERHUB_TOKEN.

## Versionamento

Tags semânticas: v1, v1.0.0