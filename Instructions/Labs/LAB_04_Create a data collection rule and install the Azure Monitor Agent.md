---
lab:
  title: Exercício 04 – Criar uma regra de coleta de dados e instalar o Agente do Azure Monitor
  module: Module 05 - Collect guest operating system monitoring data from Azure and hybrid virtual machines using Azure Monitor Agent
---


>**Observação**: para concluir este laboratório, você precisará ter uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) na qual você tem acesso administrativo. 


As DCRs (regras de coleta de dados) especificam os dados a serem coletados, enquanto o Agente do Azure Monitor aplica essas regras para coletar logs e métricas de máquinas virtuais no Azure, em outras nuvens ou no local. Juntas, elas permitem o monitoramento consistente e centralizado em diferentes ambientes.

---

## Tarefas de habilidades

- Crie e defina uma regra de coleta de dados.

- Selecione os recursos de destino para coleta de dados.

- Instale o Agente do Azure Monitor.
  
- Configure as origens e destinos de dados.

- Selecione os tipos de fonte de dados e os dados a serem coletados.

- Escolha um destino de entrega de dados.

## Instruções para o exercício 

### Criar e definir uma regra de coleta de dados e instalar o Agente do Azure Monitor.

>**Observação**: crie a regra de coleta de dados na mesma região que o workspace do Log Analytics ou o workspace do Azure Monitor. Você pode associá-la a computadores ou contêineres de qualquer assinatura ou grupo de recursos no locatário. O Agente do Azure Monitor será instalado automaticamente nos recursos virtuais do Azure.

1. Abra uma sessão do navegador e entre no [menu do portal do Azure](https://portal.azure.com/).
  
3. Na caixa de pesquisa na parte superior do portal, digite **regras de coleta de dados**. Selecione **Regras de coleta de dados** nos resultados da pesquisa.
  
4. Na página **Regras de coleta de dados**, clique em **+ Criar**.
  
    ![imagem](https://github.com/user-attachments/assets/a472bc6f-fa96-4615-a67c-c99e8b9ce7a4)

5. Na página **Básico** da **folha Criar regra de coleta de dados**, especifique as seguintes configurações (deixe as outras com os valores padrão):

    |Configuração|Valor|
    |---|---|
    |**Detalhes da regra**|
    |Nome da Regra|**dcr-1**|
    |Assinatura|Selecione sua assinatura.|
    |Resource group|**az-rg-1**|
    |Região|**Leste dos EUA**|
    |Tipo de Plataforma|**Windows**|
    |Ponto de extremidade da coleta de dados|Mantenha a configuração padrão como nenhum|

   ![imagem](https://github.com/user-attachments/assets/6c63c48f-f7a9-4fb2-8fc0-e22084cd5013)

6. Clique no botão na parte inferior da página **Básico** rotulado **Avançar: Recursos >** para continuar.
   
7. Na página **Recursos**, clique em **+ Adicionar recursos**.

   ![imagem](https://github.com/user-attachments/assets/7e45996b-478b-4be4-9df3-df6127da6cb4)

8. No modelo **Selecionar um escopo**, marque a caixa **Assinatura** no **Escopo**.

   ![imagem](https://github.com/user-attachments/assets/0d228e47-039e-4418-ae66-025957e368bc)

9. Na parte inferior do modelo **Selecionar um escopo**, clique em **Aplicar**.
  
10. Na parte inferior da página **Recursos**, clique em **Avançar: Coletar e entregar >**.

    ![imagem](https://github.com/user-attachments/assets/95556211-654f-4810-98a0-5cd8fac13bff)  

11. Na página **Coletar e entregar**, clique em **+ Adicionar fonte de dados**.

    ![imagem](https://github.com/user-attachments/assets/8274b0c1-8617-4889-9aef-78e050f2bd00)

12. No modelo **Adicionar fonte de dados**, em **Tipo de fonte de dados**, selecione as configurações a seguir:
    
    |Configuração|Valor|
    |---|---|
    |**Adicionar fonte de dados**|
    |Selecione o tipo de fonte de dados e os dados a serem coletados para os recursos.|
    |Tipo de fonte de dados*|**Logs de eventos do Windows**|
    |Escolha Básico para habilitar a coleta de logs de eventos.|
    |Configure os logs e níveis de eventos a serem coletados:|
    |Aplicativo|**Crítico**, **Erro**, **Aviso**|
    |Segurança|**Auditoria realizada**, **Falha na auditoria**|
    |Sistema|**Crítico**, **Erro**, **Aviso**|

    ![imagem](https://github.com/user-attachments/assets/33039994-0613-40f4-9c55-03f795b38b9b)

13. Na parte inferior do modelo **Adicionar fonte de dados**, clique em **Avançar: Destino >**.

14. No modelo **Adicionar fonte de dados**, na guia **Destino**, selecione as configurações a seguir.
    
    |Configuração|Valor|
    |---|---|
    |**Adicionar fonte de dados**|
    |Destino|**+ Adicionar destino**|
    |Tipo de destino|**Logs do Azure Monitor**|
    |Subscription|Selecione sua Assinatura.|
    |Detalhes do Destino|**azwrkspc1a (az-rg-1**)|

     ![imagem](https://github.com/user-attachments/assets/dc2d2906-4a57-4df9-a33c-fd6ae34a8457)

15. Na parte inferior do modelo **Adicionar fonte de dados**, selecione **Adicionar fonte de dados**.

16. Na parte inferior da página **Coletar e entregar**, selecione **Revisar + criar**.

    ![imagem](https://github.com/user-attachments/assets/4277089c-971c-4334-a49d-6ac6bfe93ff4)

17. Na parte inferior da página **Revisar + criar** clique em **Criar**.

    ![imagem](https://github.com/user-attachments/assets/b532f92e-af10-4b4d-bb52-10d15ad38d4a)

> **Resultados**: você criou uma regra de coleta de dados e instalou o Agente do Azure Monitor.
