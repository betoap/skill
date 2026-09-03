# Perfil de stack

MaestrIA produz este artefato durante a análise arquitetural. Ele descreve o stack encontrado; não é autorização para migrá-lo.

```yaml
language:
  primary: ""
  version: ""
runtime:
  name: ""
  version: ""
application:
  framework: ""
  framework_version: ""
  architecture_style: ""
build_and_dependencies:
  build_tool: ""
  package_manager: ""
  lockfile: ""
quality:
  formatter: ""
  linter: ""
  static_analysis: []
testing:
  unit_framework: ""
  integration_or_e2e_framework: ""
  test_conventions: []
  coverage_command: ""
delivery:
  ci: ""
  containerization: ""
  deployment: ""
constraints:
  compatibility: []
  security: []
  migration_policy: "preserve-existing-stack"
evidence:
  sources: []
  confidence: confirmed
```

Preencha somente o que puder ser confirmado no projeto. Use `unknown` quando for relevante e ainda não houver evidência. Registre em `evidence.sources` os arquivos, configurações ou comandos que sustentam cada decisão. CodIA e ConfIA devem respeitar este perfil; divergências exigem retorno à MaestrIA.
