---
lab:
  title: Exercício 04 – Crie uma regra de coleta de dados e instale o Agente do Azure Monitor
  module: Module 05 - Create a data collection rule and install the Azure Monitor Agent
---


>**Observação**: para concluir este laboratório, você precisará ter uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) na qual você tem acesso administrativo. 


As DCRs (regras de coleta de dados) especificam os dados a serem coletados, enquanto o Agente do Azure Monitor aplica essas regras para coletar logs e métricas de máquinas virtuais no Azure, em outras nuvens ou no local. Juntas, elas permitem o monitoramento consistente e centralizado em diferentes ambientes.

---

## Tarefas de habilidades

- Crie e defina uma regra de coleta de dados.

- Selecione os recursos de destino para coleta de dados.
  
- Configure as origens e destinos de dados.

- Selecione os tipos de fonte de dados e os dados a serem coletados.

- Escolha um destino de entrega de dados.

## Instruções para o exercício 

### Crie e defina uma regra de coleta de dados.

>**Observação**: crie sua regra de coleta de dados na mesma região que o workspace do Log Analytics de destino ou o workspace do Azure Monitor. Você pode associar a regra de coleta de dados a computadores ou contêineres de qualquer assinatura ou grupo de recursos no locatário. 
   
1. Na caixa de pesquisa na parte superior do portal, digite Regras de coleta de dados. Selecione Regras de coleta de dados nos resultados da pesquisa.

2. Selecione **+ Criar**.

![imagem](https://github.com/user-attachments/assets/e428c441-9d8d-4460-acd9-a97e2aa2b5af)

3. Na guia **Noções básicas** da folha **Criar regra de coleta de dados**, especifique as seguintes configurações (deixe as outras com os valores padrão):

    |Configuração|Valor|
    |---|---|
    |**Detalhes da regra**|
    |Nome da Regra|**dcr-1**|
    |Assinatura|o nome da assinatura do Iginte que você está usando neste laboratório|
    |Grupo de recursos|**az-rg-1**|
    |Region|**Leste dos EUA**|
    |Tipo de Plataforma|**Windows**|
    |Ponto de extremidade da coleta de dados|*Deixe o padrão Nenhum*|

![imagem](https://github.com/user-attachments/assets/eee884f6-b20f-4d51-9310-6e755746ed9a)   

4. Clique no botão **Avançar: recursos >** para prosseguir.

5. Na guia Recursos, clique em **+ Adicionar recursos**.
  
>**Observação**: o Agente do Azure Monitor será instalado automaticamente nas máquinas virtuais (recursos) selecionadas para coletar dados.
   
![imagem](https://github.com/user-attachments/assets/619106b4-7f5e-44dd-98c7-129689ab89c0)

6. No modelo Selecionar um escopo, marque a caixa **Ignite-subscription** na seleção Escopo e clique em **Aplicar**.

![imagem](https://github.com/user-attachments/assets/c95b76cd-1515-47a5-b07b-02dcb28c0bf3)


8. Selecione **Examinar + criar**.








> **Resultados**: você criou uma regra de coleta de dados e instalou o Agente do Azure Monitor.
