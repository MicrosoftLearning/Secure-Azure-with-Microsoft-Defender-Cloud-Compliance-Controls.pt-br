---
lab:
  title: Exercício 01 – Habilitar o Defender para Nuvem na sua assinatura do Azure
  module: Module 02 - Enable Defender for Cloud on your Azure subscription
---


>**Observação**: para concluir este laboratório, você precisará ter uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) na qual você tem acesso administrativo. 


O principal objetivo deste exercício é fornecer experiência prática na configuração e habilitação do Microsoft Defender para Nuvem em uma assinatura do Azure. Isso permitirá que você monitore e proteja seus recursos de nuvem contra ameaças de segurança. 

---

## Tarefas de habilidades

- Atualizar sua assinatura do Microsoft Defender para Nuvem.
  
- Implante o Microsoft Monitoring Agent nos computadores necessários para uma cobertura abrangente.

## Instruções para o exercício

### Atualizar o Microsoft Defender para Nuvem

1. Entre no [menu do portal do Azure.](https://portal.azure.com/)

2. No portal do Azure, na caixa de texto Pesquisar recursos, serviços e documentos na parte superior da página do portal do Azure, digite Microsoft Defender para Nuvem e pressione a tecla Enter.

3. No painel do **Microsoft Defender para Nuvem**, **Introdução**, vá para a **guia Atualizar**. Role para baixo até que a seção **Selecionar assinaturas e workspaces para proteger com recursos de segurança aprimorados** esteja visível.

4. Ative o plano do Microsoft Defender selecionando sua **Assinatura** e o **Workspace do Log Analytics** que você criou no Módulo 02.

5. Clique no grande botão azul **Atualizar** na parte inferior da página.
   
    ![imagem](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/256bd584-b04f-4d5b-81a7-c83dd1af3b4f)
   
6. No painel **Microsoft Defender para Nuvem**, **Introdução**, acesse a guia **Instalar agentes** e role para baixo.

    ![imagem](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/8120ec8f-23dc-4636-bc45-b415c7894b8c)

7. Marque a caixa associada à assinatura na qual os agentes serão instalados e clique em **Instalar agentes.**

### Ações alternativas para atualizar sua assinatura do Microsoft Defender para Nuvem.

1. Navegue até **Microsoft Defender para Nuvem** e, no painel de navegação esquerdo, na seção Gerenciamento, clique em **Configurações do Ambiente.**
   
2. No painel **Microsoft Defender para Nuvem, Configurações do Ambiente**, clique em **Expandir tudo**, role para baixo até que sua assinatura seja exibida e clique na assinatura relevante.

3. Na folha **Configurações, planos do Defender**, selecione **Habilitar todos os planos** e clique em **Salvar.**

   ![imagem](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Defender-for-Cloud-regulatory-compliance-controls/assets/91347931/4b684851-98ae-4720-a3e3-afa99aab8c43)




   

   
> **Resultados**: você atualizou e habilitou o Defender para Nuvem em sua assinatura do Azure.
