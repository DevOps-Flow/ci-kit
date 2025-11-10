# setup-java-maven

Prepara o ambiente Java + Maven com **cache do repositório local (`~/.m2/repository`)** para acelerar builds.

## Quando usar
- Antes de compilar/testar projetos Maven/Quarkus.
- Em qualquer job que precise de Java + Maven + cache.

## Inputs
| Nome           | Obrigatório | Default | Descrição                      |
|----------------|-------------|---------|--------------------------------|
| `java_version` | não         | `21`    | Versão do Java (Temurin).      |
| `maven_version`| não         | `3.9.9` | Versão do Maven.               |

## Outputs
Nenhum.

## Exemplo de uso
```yaml
- uses: lab-safer/ci-kit/setup-java-maven@v1
  with:
    java_version: '21'
    maven_version: '3.9.9'
```

## Requisitos

- Runner Linux (Ubuntu) recomendado.

## Erros comuns

- Cache não bate: confirme a chave do cache (hashFiles('**/pom.xml')) e se os pom.xml estão versionados.

## Versionamento

- Use tags semânticas: v1, v1.0.0