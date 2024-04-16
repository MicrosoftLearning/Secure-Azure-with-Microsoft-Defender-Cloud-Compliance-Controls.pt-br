---
lab:
  title: Exercício 04 – Coletar dados de suas cargas de trabalho com o agente do Log Analytics
  module: Module 04 - Configure and integrate a Log Analytics agent and workspace in Defender for Cloud
---


>**Observação**: para concluir este laboratório, você precisará ter uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) na qual você tem acesso administrativo. 


O Defender para Nuvem coleta dados das VMs (máquinas virtuais) do Azure, dos Conjuntos de Dimensionamento de Máquinas Virtuais, dos contêineres de IaaS e de computadores não Azure (inclusive nos locais) para monitorar as vulnerabilidades e ameaças de segurança. Alguns planos do Defender exigem componentes de monitoramento para coletar dados de suas cargas de trabalho. Quando o agente do Log Analytics estiver habilitado, o Defender para Nuvem implantará o agente em todas as VMs do Azure compatíveis, bem como naquelas que forem criadas. 

---

## Tarefas de habilidades

- Use os padrões de agente do Log Analytics para seu tipo de agente.

- Selecione o workspace.
  
- Defina o nível dos dados de evento de segurança a serem armazenados no nível do workspace.

## Instruções para o exercício 

### Configure a integração com o agente do Log Analytics.

>**Observação**: quando o agente do Log Analytics estiver habilitado, o Defender para Nuvem implantará o agente em todas as VMs do Azure compatíveis, bem como naquelas que forem criadas. 

1. Abra uma sessão do navegador e entre no [menu do portal do Azure](https://portal.azure.com/).
   
2. No menu do Defender para Nuvem, abra **Configurações de ambiente**.

4. Selecione sua assinatura.

5. Na coluna Configurações e cobertura de monitoramento dos planos do Defender, selecione **Configurações e monitoramento.**

7. Na linha Log Analytics, na coluna Configuração, clique em **Editar configuração.**

8. No modelo de configuração de provisionamento automático, conclua as seguintes ações:

   - Em Seleção do workspace, clique em **Workspace personalizado.**

   - Clique no **menu suspenso** e **selecione** seu workspace criado anteriormente.

   - Em **Armazenamento de eventos de segurança**, clique no **menu suspenso** e selecione **Todos os eventos.**

   - Na parte inferior do modelo de provisionamento automático, clique em **Aplicar.**
   
![imagem](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/c1c812e7-b5ca-4caa-b8e6-34a6e4b325fd)




> **Resultados**: você configurou o agente e o workspace do Log Analytics no Microsoft Defender para Nuvem.
