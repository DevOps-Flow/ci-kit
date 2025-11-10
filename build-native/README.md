# build-native

Compila **Quarkus Native** usando `-Pnative` (GraalVM/Mandrel via container-build) e publica o binário `*-runner` como artifact.

## Quando usar
- Para gerar o binário nativo do serviço antes de montar a imagem Docker final.

## Inputs
| Nome            | Obrigatório | Default        | Descrição                |
|-----------------|-------------|----------------|--------------------------|
| `artifact_name` | não         | `native-runner`| Nome do artifact gerado. |

## Outputs
Nenhum.

## Exemplo de uso
```yaml
- uses: lab-safer/ci-kit/build-native@v1
  with:
    artifact_name: native-runner
```

## Requisitos

- Java/Maven já configurados (use setup-java-maven antes).

- Docker disponível (para -Dquarkus.native.container-build=true).

## Erros comuns

- Falta de memória/CPU no runner → aumentar recursos do job.

- Dependências pesadas → combine com cache Maven (setup-java-maven).

## Versionamento

- Tags semânticas: v1, v1.0.1