# export-image-base

Valida e exporta o nome base da imagem Docker (ex.: `usuario/repositorio`) a partir da variável de ambiente `DOCKER_IMAGE`  
ou de um input explícito `docker_image`.

Usada para padronizar a definição do nome da imagem dentro de pipelines reutilizáveis sem repetir lógica em vários jobs.

---

## 🧩 Quando usar
Antes de qualquer etapa que construa ou atualize imagens Docker (ex.: build/push/update-manifest).  
Essa action garante que o nome da imagem é válido e consistente.

---

## ⚙️ Inputs

| Nome | Obrigatório | Descrição |
|------|-------------|------------|
| `docker_image` | Não | Nome base da imagem (ex.: `usuario/repositorio`). Se não informado, utiliza a variável de ambiente `DOCKER_IMAGE` herdada do repositório chamador. |

---

## 📤 Outputs

| Nome | Descrição |
|------|------------|
| `image` | Nome base validado da imagem Docker (sem tag). |

---

## 🧱 Exemplo de uso

```yaml
- name: Resolve image base
  id: img
  uses: DevOps-Flow/ci-kit/export-image-base@v1
  with:
    docker_image: ${{ vars.DOCKER_IMAGE }}

- name: Build image
  uses: DevOps-Flow/ci-kit/docker-build-push@v1
  with:
    image:   ${{ steps.img.outputs.image }}
    version: 1.0.10
    dockerhub_user: ${{ secrets.DOCKERHUB_USERNAME }}
    dockerhub_token:${{ secrets.DOCKERHUB_TOKEN }}
```
## Validação

- A action checa se o nome informado segue o formato:
```usuario/repositorio```
- Permitindo apenas letras minúsculas, números, pontos (.), underscores (_) e hifens (-).
- Se o nome estiver inválido ou vazio, o job falha com mensagem de erro clara.

## Como funciona internamente

- Prioriza o valor de inputs.docker_image.
- Caso esteja vazio, usa a variável `DOCKER_IMAGE` do ambiente.
- Valida o formato com uma expressão regular.
- Exporta o resultado via `GITHUB_OUTPUT` como image.

## Versionamento

- Use tags semânticas: v1, v1.0.3, etc.
- A tag v1 pode ser movida para a última release estável.