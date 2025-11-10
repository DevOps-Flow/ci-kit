# ci-kit

Ações compostas reutilizáveis para pipelines Java/Quarkus + Docker + Kubernetes/Argo CD.

## Ações
- `setup-java-maven`: Java + Maven + cache `~/.m2`
- `resolve-image`: resolve nome da imagem Docker (com validação)
- `build-native`: build Quarkus Native e exporta artifact
- `docker-build-push`: Buildx com cache remoto (Docker Hub) + push
- `update-manifest`: atualiza `image:` no YAML com `yq` e faz commit/push (GitOps)
- `argocd-deploy`: Argo CD sync + wait + rollback GitOps

## Versionamento
- Crie tags: `v1`, `v1.0.0`…
- Use nos workflows: `uses: lab-safer/ci-kit/<action>@v1`

## Suporte/Contribuição
- PRs com testes em workflows “sandbox”.
- Mantenha compatibilidade com Ubuntu runners.