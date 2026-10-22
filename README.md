Eduardo Vieira Martins da Silva, RA: 250268
Isabelly Hipolliti Lucantonio, RA: 250284_

# DevOps — Automação com GitHub Actions

Projeto desenvolvido para demonstrar a automação de processos de desenvolvimento utilizando **Git, GitHub e GitHub Actions**.

O projeto conta com dois workflows principais: geração automática de changelog e criação de pacotes de release para download.

---

## Objetivos do projeto

- Automatizar tarefas recorrentes do ciclo de desenvolvimento.
- Registrar o histórico de alterações do projeto.
- Gerar pacotes ZIP de versões específicas.
- Disponibilizar versões para download por meio das Releases do GitHub.
- Aplicar conceitos de CI/CD utilizando GitHub Actions.

---

## 1. Changelog Automático

### O que é?

O Changelog é um arquivo que registra as alterações realizadas no projeto ao longo do tempo. Neste projeto, o arquivo `CHANGELOG.md` é gerado automaticamente a partir do histórico de commits do Git.

### Como funciona?

O workflow está localizado em:

`.github/workflows/changelog.yml`

Seu funcionamento ocorre da seguinte maneira:

1. O desenvolvedor envia alterações para a branch `main`.
2. O GitHub Actions executa o workflow.
3. O histórico de commits é consultado pelo Git.
4. O arquivo `CHANGELOG.md` é gerado com as mensagens dos commits, suas datas e seus hashes curtos.
5. Caso existam alterações no arquivo, o workflow realiza um commit automático para atualizar o changelog no repositório.

### Exemplo de resultado

```markdown
# Changelog

## Histórico de alterações

- 2026-10-22 — feat: add new feature (a1b2c3d)
- 2026-10-21 — fix: correct validation (e4f5a6b)
```

*Os commits acima são apenas exemplos ilustrativos.*

### Como executar?

O workflow é acionado automaticamente quando ocorre um `push` para a branch `main`. Também pode ser executado manualmente pela aba **Actions**, caso o arquivo esteja configurado com `workflow_dispatch`.

O resultado fica disponível no arquivo `CHANGELOG.md`, na raiz do repositório.

---

## 2. Release Package

### O que é?

O Release Package automatiza a criação de um arquivo ZIP contendo os arquivos versionados do projeto. O pacote é anexado à Release correspondente no GitHub, permitindo que qualquer pessoa com acesso ao repositório faça o download da versão desejada.

### Como funciona?

O workflow está localizado em:

`.github/workflows/release-package.yml`

O processo ocorre da seguinte forma:

1. O desenvolvedor cria uma tag de versão, como `v1.0.0`.
2. A tag é enviada ao GitHub.
3. O GitHub Actions identifica a versão e acessa o conteúdo correspondente no Git.
4. O comando `git archive` compacta os arquivos versionados em um ZIP.
5. O GitHub CLI (`gh`) envia o pacote para a Release correspondente.
6. O arquivo fica disponível na seção **Assets** da Release.

### Exemplo de pacote gerado

```text
Trabalho_devops-v1.0.0.zip
```

O pacote contém os arquivos rastreados pelo Git naquela versão, organizados em uma pasta com o nome do projeto e da tag.

Arquivos não versionados e o histórico interno da pasta `.git` não são incluídos.

### Como gerar uma nova versão?

Crie uma tag Git e envie-a ao repositório:

```bash
git tag v1.1.0
git push origin v1.1.0
```

A publicação da tag aciona o workflow automaticamente.

**Importante:** para que o pacote seja anexado a uma Release existente, a Release correspondente à tag deve estar publicada. O workflow também permite execução manual, informando a tag desejada.

### Onde baixar o pacote?

Após a execução bem-sucedida:

1. Acesse a aba **Releases** do repositório.
2. Abra a versão desejada.
3. Localize a seção **Assets**.
4. Clique no arquivo ZIP para realizar o download.

Exemplo de arquivo publicado:

`Trabalho_devops-v1.0.0.zip`

---

## Estrutura do projeto

```text
Trabalho_devops/
├── .github/
│   └── workflows/
│       ├── hello.yml
│       ├── changelog.yml
│       └── release-package.yml
├── CHANGELOG.md
└── README.md
```

- `hello.yml`: workflow inicial de CI.
- `changelog.yml`: automação do histórico de alterações.
- `release-package.yml`: criação e publicação de pacotes ZIP.
- `CHANGELOG.md`: histórico de commits gerado automaticamente.
- `README.md`: documentação do projeto.

---

## Tecnologias utilizadas

- **Git:** controle de versão e gerenciamento do histórico de commits.
- **GitHub:** hospedagem do repositório, gerenciamento de tags e publicação de Releases.
- **GitHub Actions:** execução automatizada dos workflows.
- **GitHub CLI (`gh`):** publicação do arquivo ZIP na Release.
- **Bash e comandos Git:** geração do pacote e execução das tarefas de automação.

Não são necessários scripts externos ou ferramentas de terceiros para gerar o changelog e o pacote ZIP.

---

## Resultados alcançados

Com a implementação dos dois workflows, o projeto permite:

- Manter um histórico de alterações atualizado automaticamente.
- Reduzir tarefas manuais no processo de versionamento.
- Gerar pacotes ZIP de versões específicas.
- Disponibilizar versões para download diretamente no GitHub.
- Aplicar práticas de automação e versionamento em um fluxo de DevOps.

---

## Autor

**linkdonis**

Projeto acadêmico de DevOps desenvolvido com Git, GitHub e GitHub Actions.
