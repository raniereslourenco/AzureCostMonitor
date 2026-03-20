# Controle de Versionamento em Azure Databricks 🚀

Este repositório documenta o fluxo de trabalho para controle de versão de notebooks utilizando a integração nativa do Azure Databricks com Git (Databricks Repos).

## 📋 Processo de Configuração

O versionamento no Databricks não deve ser feito via upload manual de arquivos, mas sim através da funcionalidade **Repos**.

1. **Configuração de Git Credentials**: 
   - Vá em `User Settings` > `Linked Accounts`.
   - Adicione seu Personal Access Token (PAT) do Azure DevOps ou GitHub.
2. **Clonando o Repositório**:
   - No menu lateral, clique em `Repos` > `Add Repo`.
   - Insira a URL do repositório Git.

---

## 💡 Insights e Boas Práticas

### 1. Formato de Arquivo (.py vs .ipynb)
Ao versionar notebooks, o Databricks prefere converter internamente para arquivos `.py` com anotações de célula (ex: `# COMMAND ----------`). Isso é excelente para:
- **Code Reviews**: Facilita a leitura de diffs no Git.
- **Linter**: Permite rodar ferramentas de análise estática mais facilmente.

### 2. Separação de Ambientes
Trabalhe sempre com **Branches**:
- `main`: Código produtivo (somente via Pull Request).
- `develop`: Integração de novas features.
- `feature/nome-da-tarefa`: Desenvolvimento isolado.

### 3. Variáveis de Ambiente e Segredos
**Nunca** versione senhas ou tokens no código do notebook. Utilize o **Azure Key Vault** integrado aos **Databricks Secrets**.
```python
# Forma correta
dbutils.secrets.get(scope="meu-escopo", key="api-key")
