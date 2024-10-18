---
lab:
  title: Exercício 03 – Criar um workspace do Log Analytics
  module: Module 04 - Create a Log Analytics workspace
---


>**Observação**: para concluir este laboratório, você precisará ter uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) na qual você tem acesso administrativo. 


Quando você coleta logs e dados, as informações são armazenadas em um workspace. Um workspace tem uma ID de workspace e uma ID de recurso exclusivas. O nome do workspace precisa ser exclusivo para um determinado grupo de recursos. Depois de criar um workspace, configure fontes de dados e soluções para armazenar seus dados nelas. 

---

## Tarefa de habilidades

- Criar um espaço de trabalho do Log Analytics.
- Associe o workspace a um grupo de recursos existente.
- Especifique uma região específica para implantar o workspace.

## Instruções para o exercício 

### Use o menu de workspaces do Log Analytics para criar um workspace.

1. Abra uma sessão do navegador e entre no [menu do portal do Azure](https://portal.azure.com/).
   
2. No menu do portal do Azure, insira **workspaces do Log Analytics** na caixa de pesquisa. Quando você começa a digitar, a lista é filtrada com base em sua entrada. Escolha **workspaces do Log Analytics**.

4. Selecione **Criar**.

5. Na guia **Noções básicas** em **Criar workspace do Log Analytics**, insira ou selecione estas informações:
   
   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Insira **az-rg-1.** Selecione **OK**|
   |**Detalhes da instância**|
   |Nome|Digite **azwrkspc1a.**|
   |Region|Selecione **Leste dos EUA**.|

6. Selecione a guia **Revisar + criar** ou selecione o botão azul Revisar + criar na parte inferior da página.
  
8. Selecione **Criar**.

> **Resultados:** você criou um workspace do Log Analytics para coletar dados de recursos do Azure.
