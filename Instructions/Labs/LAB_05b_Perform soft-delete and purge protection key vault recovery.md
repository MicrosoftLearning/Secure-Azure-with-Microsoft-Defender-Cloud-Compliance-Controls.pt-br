---
lab:
  title: Exercício 05b – Configurar o gerenciamento de recuperação do Azure Key Vault com exclusão temporária e proteção contra limpeza
  module: Module 05 - Perform soft-delete and purge protection key vault recovery
---


>**Observação**: para concluir este laboratório, você precisará ter uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) na qual você tem acesso administrativo. 


Você pode usar a proteção contra limpeza para impedir a exclusão de seu cofre de chaves, chaves, segredos e certificados por uma atividade interna mal-intencionada. Pense nisso como uma lixeira com um bloqueio baseado em tempo. É possível recuperar itens em qualquer ponto durante o período de retenção configurável. Não será possível excluir ou limpar permanentemente um cofre de chaves até que o período de retenção tenha decorrido. Depois que o período de retenção expirar, o cofre de chaves ou o objeto do cofre de chaves será limpo automaticamente.

---

## Tarefas de habilidades

- Verifique se a exclusão temporária está disponível para um cofre de chaves e habilite a exclusão temporária.

- Listar, recuperar ou limpar um cofre de chaves com exclusão temporária.

- Listar, recuperar ou limpar segredos, chaves e certificados excluídos temporariamente.

## Instruções para o exercício 

### Verifique se a exclusão reversível está disponível para um cofre de chaves e habilite a exclusão reversível

1. Abra uma sessão do navegador e entre no [menu do portal do Azure](https://portal.azure.com/).
   
2. Selecione seu cofre de chaves.

3. Clique no painel **Propriedades**.

4. Verifique se o botão de opção ao lado de exclusão temporária está definido como **Habilitar proteção contra limpeza.**

5. Se a exclusão temporária não estiver habilitada no cofre de chaves, clique no botão de opção para habilitá-la e clique em **Salvar.**

![imagem](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/06131a60-7f00-4764-a424-87ea41a78394)


### Listar, recuperar ou limpar um cofre de chaves com exclusão temporária.

1. Abra uma sessão do navegador e entre no [menu do portal do Azure](https://portal.azure.com/).
   
2. Clique na barra de pesquisa na parte superior da página.

3. Pesquise pelo serviço **Key Vault**. Não clique em um cofre de chaves individual.

4. Na parte superior da tela, clique na opção "Gerenciar cofres excluídos"

5. Será aberto um painel de contexto do lado direito da tela.

6. Selecione sua assinatura.

7. Se o cofre de chaves foi excluído de forma reversível, ele aparecerá no painel de contexto à direita.

8. Se houver muitos cofres, será possível clicar em "Carregar mais" na parte inferior do painel de contexto ou usar a CLI ou o PowerShell para obter os resultados.

9. Quando encontrar o cofre que deseja **recuperar** ou **limpar**, marque a **caixa de seleção** ao lado dele.

10. Selecione a opção recuperar na parte inferior do painel de contexto se desejar recuperar o cofre de chaves.

11. Selecione a opção limpar se desejar excluir permanentemente o cofre de chaves.

![imagem](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/f41c0673-3832-4d3f-8b05-48e46e6c2282)


### Listar, recuperar ou limpar segredos, chaves e certificados excluídos temporariamente.

1. Abra uma sessão do navegador e entre no [menu do portal do Azure](https://portal.azure.com/).
   
2. Selecione seu cofre de chaves.

3. Selecione a folha correspondente ao tipo de segredo que deseja gerenciar (chaves, segredos ou certificados).

4. Na parte superior da tela, clique em "Gerenciar excluídos (chaves, segredos ou certificados)

5. Será exibido um painel de contexto do lado direito da tela.

6. Se seu segredo, chave ou certificado não aparecer na lista, ele não estará no estado de exclusão reversível.

7. Selecione o segredo, a chave ou o certificado que deseja gerenciar.

8. Selecione a opção para recuperar ou limpar na parte inferior do painel de contexto.

![imagem](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/dab95f78-1642-4883-b56f-70e1e5320d45)


  > **Resultados**: você executou o gerenciamento de recuperação do Azure Key Vault com exclusão temporária e proteção contra limpeza no portal do Azure.
