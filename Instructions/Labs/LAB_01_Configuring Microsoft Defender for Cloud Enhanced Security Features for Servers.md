---
lab:
  title: Exercício 01 – Configurar Recursos de Segurança aprimorados para Servidores do Microsoft Defender para Nuvem
  module: Module 02 - Enable Defender for Cloud on Your Azure Subscription
---


>**Observação**: para concluir este laboratório, você precisará ter uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) na qual você tem acesso administrativo. 


O principal objetivo deste exercício é fornecer experiência prática de configuração e habilitação do Plano 2 do Microsoft Defender para servidores em uma assinatura do Azure. Isso permitirá que você monitore e proteja seus recursos de nuvem contra ameaças de segurança. 

---

## Tarefas de habilidades

- Configurar Recursos de Segurança aprimorados para Servidores do Microsoft Defender para Nuvem
  
- Examine os recursos de segurança aprimorados do Plano 2 do Microsoft Defender para Servidores

## Instruções para o exercício

### Configurar Recursos de Segurança aprimorados para Servidores do Microsoft Defender para Nuvem

1. Entre no [menu do portal do Azure.](https://portal.azure.com/)

2. Na caixa de texto Pesquisar recursos, serviços e documentos na parte superior da página do portal do Azure, digite **Microsoft Defender para Nuvem** e pressione a tecla **Enter**.

3. Na folha **Gerenciamento** do **Microsoft Defender para Nuvem**, acesse **Configurações de ambiente**. Expanda as pastas de configurações do ambiente até que a seção **assinatura** seja exibida e clique na **assinatura** para exibir os detalhes.

   ![imagem](https://github.com/user-attachments/assets/32d2168e-458f-4872-9bf8-e8f050f24751)
   
3. Na folha **Configurações**, em **Planos do Defender**, expanda **CWP (Proteção de Carga de Trabalho na Nuvem)**.

4. Na lista **Plano de CWP (Proteção de Carga de Trabalho na Nuvem)**, selecione **Servidores**. No lado direito da página, altere o **Status** de **Desativado** para **Ativado** e clique em **Salvar**.

5. Para examinar os detalhes do **Plano 2 do Microsoft Defender para Servidores**, escolha **Alterar plano >**.

   Observação: habilitar o plano de Servidores de CWP (Proteção de Carga de Trabalho na Nuvem) de Desativado para Ativado habilita o Plano 2 do Microsoft Defender para servidores.

   ![imagem](https://github.com/user-attachments/assets/869a38e4-464e-4be0-b02e-ce1b96f02978)
   
> **Resultados**: você habilitou o Plano 2 do Microsoft Defender para servidores na sua assinatura.
