---
lab:
  title: Exercício 06b – Habilitar a exclusão temporária no Azure Key Vault
  module: Module 07 - Configure Azure Key Vault networking settings
---


>**Observação**: para concluir este laboratório, você precisará ter uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) na qual você tem acesso administrativo. 


A exclusão de um cofre de chaves sem a exclusão temporária habilitada permanentemente exclui todos os segredos, as chaves e os certificados armazenados no cofre de chaves. A exclusão acidental de um cofre de chaves pode levar à perda permanente de dados. A exclusão temporária permite recuperar um cofre de chaves excluído acidentalmente por um período de retenção configurável.

---

## Tarefas de habilidades

- Verifique se a exclusão temporária está disponível para um cofre de chaves e habilite a exclusão temporária.

## Instruções para o exercício 

### Verifique se a exclusão reversível está disponível para um cofre de chaves e habilite a exclusão reversível

1. Abra uma sessão do navegador e entre no [menu do portal do Azure](https://portal.azure.com/).
  
2. Na caixa de pesquisa, na parte superior do portal, insira **cofres de chaves**. Selecione **Cofres de chaves** nos resultados da pesquisa.
   
3. Navegue até o cofre de chaves criado anteriormente.

4. Na folha **Configurações**, selecione **Propriedades**.

5. Verifique se o botão de opção ao lado da exclusão temporária está definido como **Ativar proteção contra limpeza (impor um período de retenção obrigatório para cofres e objetos de cofre excluídos).**

6. Se a exclusão temporária não estiver habilitada no cofre de chaves, clique no botão de opção **Habilitar proteção contra limpeza (impor um período de retenção obrigatório para cofres e objetos de cofre excluídos)** para habilitar a exclusão temporária e clique em **Salvar**.

   ![imagem](https://github.com/user-attachments/assets/8cc1d810-5a15-43fb-9dd8-1484af65897e)

> **Resultados**: você habilitou a exclusão temporária, garantindo que os recursos excluídos sejam retidos por 90 dias (por padrão) e possam ser recuperados, desfazendo efetivamente a exclusão por meio do portal do Azure.
