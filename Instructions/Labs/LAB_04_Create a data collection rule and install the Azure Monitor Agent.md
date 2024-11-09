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

1. Na caixa de pesquisa na parte superior do portal, digite **regras de coleta de dados**. Selecione **Regras de coleta de dados** nos resultados da pesquisa.
  
2. Na página **Regras de coleta de dados**, clique em **+ Criar**.
  
   ![imagem](https://github.com/user-attachments/assets/99b9ac51-f2f4-466f-80bb-79d74874b573)

3. Na página **Básico** da **folha Criar regra de coleta de dados**, especifique as seguintes configurações (deixe as outras com os valores padrão):

    |Configuração|Valor|
    |---|---|
    |**Detalhes da regra**|
    |Nome da Regra|**dcr-1**|
    |Assinatura|Selecione sua assinatura.|
    |Resource group|**az-rg-1**|
    |Region|**Leste dos EUA**|
    |Tipo de Plataforma|**Windows**|
    |Ponto de extremidade da coleta de dados|Mantenha a configuração padrão como nenhum|

    ![imagem](https://github.com/user-attachments/assets/35c527cf-499d-44b9-966f-0114b8643ef2)

4. Clique no botão na parte inferior da página **Básico** rotulado **Avançar: Recursos >** para continuar.
   
5. Na página **Recursos**, clique em **+ Adicionar recursos**.

    ![imagem](https://github.com/user-attachments/assets/6aabf2c9-bea2-47c1-9b0b-bf131cdec4e3)

6. No modelo **Selecionar um escopo**, marque a caixa **Assinatura** no **Escopo**.

    ![imagem](https://github.com/user-attachments/assets/2215e8cd-5047-4fc6-91ba-b2c645571bbd)

7. Na parte inferior do modelo **Selecionar um escopo**, clique em **Aplicar**.
  
8. Na parte inferior da página **Recursos**, clique em **Avançar: Coletar e entregar >**.

    ![imagem](https://github.com/user-attachments/assets/717226c3-5ce0-454f-93a4-11b0e67d5a23)

9. Na página **Coletar e entregar**, clique em **+ Adicionar fonte de dados**.

    ![imagem](https://github.com/user-attachments/assets/0809cf5b-a460-40d1-8508-e42ba7ce78c1)

10. No modelo **Adicionar fonte de dados**, em **Tipo de fonte de dados**, selecione as configurações a seguir.
    
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

    ![imagem](https://github.com/user-attachments/assets/5bc891ea-8cef-4baa-95c4-a432364179b1)

12. Na parte inferior do modelo **Adicionar fonte de dados**, clique em **Avançar: Destino >**.
   
13. No modelo **Adicionar fonte de dados**, na guia **Destino**, selecione as configurações a seguir.
    
    |Configuração|Valor|
    |---|---|
    |**Adicionar fonte de dados**|
    |Destino|**+ Adicionar destino**|
    |Tipo de destino|**Logs do Azure Monitor**|
    |Assinatura|Selecione sua Assinatura.|
    |Detalhes do Destino|**azwrkspc1a (az-rg-1**)|

    ![imagem](https://github.com/user-attachments/assets/e00c17c8-5a70-4caa-8504-92f482cc5e57)

14. Na parte inferior do modelo **Adicionar fonte de dados**, selecione **Adicionar fonte de dados**.

    ![imagem](https://github.com/user-attachments/assets/4277089c-971c-4334-a49d-6ac6bfe93ff4)

15. Na parte inferior da página **Coletar e entregar**, selecione **Revisar + criar**.

    ![imagem](https://github.com/user-attachments/assets/0235fed9-6309-444c-9269-b9dbd1118b63)

16. Na parte inferior da página **Revisar + criar** clique em **Criar**.

> **Resultados**: você criou uma regra de coleta de dados e instalou o Agente do Azure Monitor.
