---
lab:
  title: Exercício 02 – Criar uma infraestrutura de rede virtual
  module: Module 03 - Filter network traffic with a network security group using the Azure portal
---


>**Observação**: para concluir este laboratório, você precisará ter uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) na qual você tem acesso administrativo. 


É possível usar um grupo de segurança de rede para filtrar o tráfego de rede de entrada e saída dos recursos do Azure em uma rede virtual do Azure. Grupos de segurança de rede contêm regras de segurança que filtram o tráfego por endereço IP, porta e protocolo. Quando um grupo de segurança de rede é associado a uma sub-rede, as regras de segurança são aplicadas aos recursos implantados nessa sub-rede.

## Diagrama de arquitetura

![imagem](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/1bfec315-129b-48a9-9c35-1f21c837068f)

---

## Tarefas de habilidades

- Criar um grupo de segurança de rede e regras de segurança.
  
- Criar grupos de segurança de aplicativos.
  
- Criar uma rede virtual e associar um grupo de segurança de rede a uma sub-rede.
  
- Implantar máquinas virtuais e associar as respectivas interfaces de rede com os grupos de segurança de aplicativos.

## Instruções para o exercício 

### Criar um grupo de recursos e uma rede virtual do Azure.

>**Observação**: a tarefa a seguir cria uma rede virtual com uma sub-rede de recursos.

1. Abra uma sessão do navegador e entre no [menu do portal do Azure](https://portal.azure.com/).             
   
2. Na caixa de pesquisa, na parte superior do portal, digite **redes virtuais**. Selecione **Redes virtuais** nos resultados da pesquisa.

3. Na página **Redes virtuais**, selecione **+ Criar**.

4. Na guia **Informações Básicas** em **Criar rede virtual**, insira ou selecione as informações a seguir:
   
   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Insira **az-rg-1.**|
   |**Detalhes da instância**|
   |Nome da rede virtual|Insira **vnet-1**.|
   |Região|Selecione **(EUA) Leste dos EUA**.|  
    
5. Selecione **Avançar** para prosseguir para a guia **Segurança**.
  
6. Selecione **Avançar** para prosseguir para a guia **Endereços IP**.

7. Na caixa de espaço de endereço em **Sub-redes**, selecione a sub-rede **padrão**.

8. No modelo **Editar sub-rede**, insira ou selecione as seguintes informações:

   |Configuração|Valor|
   |---|---|
   |**Detalhes da sub-rede**|
   |Finalidade da sub-rede|Deixe a configuração padrão como Padrão.|
   |Nome|Insira **sub-rede-1.**|
   |Endereço inicial|Deixe a configuração padrão como 10.0.0.0/16.|
   |Tamanho|Deixe as configurações padrão como /24 (256 endereços).|

    ![imagem](https://github.com/user-attachments/assets/82076f64-6a7f-4235-942d-d83e32ed6ea1)

10. Selecione **Salvar**.

11. Selecione **Examinar + criar** na parte inferior da tela e, quando a validação for aprovada, selecione **Criar**.

     ![imagem](https://github.com/user-attachments/assets/c53a04e4-d760-4e28-b998-1d48a56702f1)

### Crie um grupo de segurança de aplicativos para permitir agrupar servidores com funções semelhantes, como servidores Web.

Um ASG (grupo de segurança do aplicativo) permite agrupar servidores com funções semelhantes, como servidores Web.

1. Na caixa de pesquisa, na parte superior do portal, insira **Grupos de segurança do aplicativo**. Selecione **Grupos de segurança do aplicativo** nos resultados da pesquisa.

2. Na página **Grupos de segurança do aplicativo**, clique em **+ Criar**.

3. Na guia **Básico** de **Criar um grupo de segurança do aplicativo**, insira ou selecione estas informações:
   
   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Selecione **az-rg-1**.|
   |**Detalhes da instância**|
   |Nome|Insira **asg-web**.|
   |Region|Selecione **Leste dos EUA**.|  
    
4. Selecione **Examinar + criar**.

5. Selecione **Criar**.

6. Repita as etapas anteriores especificando os valores a seguir:
    
   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Selecione **az-rg-1**.|
   |**Detalhes da instância**|
   |Nome|Insira **asg-mgmt**.|
   |Region|Selecione **Leste dos EUA**.|

7. Selecione **Examinar + criar**.

8. Selecione **Criar**.

### Crie um grupo de segurança de rede para proteger o tráfego de rede na sua rede virtual.

Um NSG (grupo de segurança de rede) protege o tráfego de rede na sua rede virtual.

1. Na caixa de pesquisa na parte superior do portal, digite **grupos de segurança de rede**. Selecione **Grupos de segurança de rede** nos resultados da pesquisa.

>**Observação**: nos resultados da pesquisa para Grupos de segurança de rede, você poderá ver os Grupos de segurança de rede (clássico). Selecione Grupos de segurança de rede.

2. Na página **Grupos de segurança de rede**, selecione **+ Criar**.

3. Na guia **Básico** em **Criar grupo de segurança de rede**, insira ou selecione estas informações:
   
   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Selecione **az-rg-1**.|
   |**Detalhes da instância**|
   |Nome|Insira **nsg-1**.|
   |Region|Selecione **Leste dos EUA**.|  
    
4. Selecione **Examinar + criar**.

5. Selecione **Criar**.

### Associar o grupo de segurança de rede à sub-rede

>**Observação**: nesta tarefa, você associará o grupo de segurança de rede à sub-rede da rede virtual criada anteriormente.

1. Na caixa de pesquisa na parte superior do portal, digite **grupos de segurança de rede**. Selecione **Grupos de segurança de rede** nos resultados da pesquisa.
   
2. Selecione **nsg-1**.

3. Selecione **Sub-redes** na seção **Configurações** da **nsg-1**.

4. Na página **nsg-1 |Sub-redes**, clique em + **Associar**:

   ![imagem](https://github.com/user-attachments/assets/bfc18dd3-3345-4c05-9981-4f479d5f7c7e)

6. Em **Associar sub-rede**, selecione **vnet-1 (taz-rg-1)** para **Rede virtual**.

7. Selecione **sub-rede-1** para **Sub-rede** e, em seguida, selecione **OK**.

### Crie regras de segurança para o grupo de segurança de rede com a sub-rede da rede virtual criada anteriormente.

1. Selecione **Regras de segurança de entrada** na seção **Configurações** do **nsg-1**.
   
2. Na página **nsg-1 | Regras de segurança de entrada**, clique em + **Adicionar**.

3. Crie uma regra de segurança que permita o acesso das portas 80 e 443 ao grupo de segurança de aplicativos **asg-web**. Na página **Adicionar regra de segurança de entrada**, insira ou selecione as estas informações:

   |Configuração|Valor|
   |---|---|
   |Fonte|Mantenha o padrão de **Any**.|
   |Intervalos de portas de origem|Deixe os intervalos de porta da configuração padrão.|
   |Destino|Selecione **Grupo de segurança do aplicativo**.|
   |Grupo de segurança do aplicativo de destino|Selecione **asg-web**.|
   |Serviço|Deixe a configuração padrão como Personalizado.|
   |Intervalos de portas de destino|Insira **80,443**.|
   |Protocolo|selecione **TCP**.|
   |Ação|Deixe as configurações padrão como Permitir.|
   |Prioridade|Deixe a configuração padrão como 100.|
   |Nome|Insira **allowweball**.|

4. Selecione **Adicionar**.

5. Conclua as etapas anteriores com as informações a seguir:

   |Configuração|Valor|
   |---|---|
   |Fonte|Mantenha o padrão de **Any**.|
   |Intervalos de portas de origem|Deixe os intervalos de porta da configuração padrão.|
   |Destino|Selecione **Grupo de segurança do aplicativo**.|
   |Grupo de segurança do aplicativo de destino|Selecione **asg-mgmt**.|
   |Serviço|Selecione **RDP**.|
   |Intervalos de portas de destino|Deixe a configuração padrão como 3389.|
   |Protocolo|Deixe a configuração padrão como TCP.|
   |Ação|Deixe a configuração padrão como Permitir.|
   |Prioridade|Deixe a configuração padrão como 110.|
   |Nome|Insira **allowrdpall**.|
   
6. Selecione **Adicionar**.

### Crie duas VMs (máquinas virtuais) na rede virtual criada anteriormente.

1. Na caixa de pesquisa na parte superior do portal, insira **máquinas virtuais**. Selecione **Máquinas virtuais** nos resultados da pesquisa.

2. Em **Máquinas virtuais**, selecione **+ Criar** e, em seguida, **Máquina virtual do Azure**.
   
3. Em **Criar máquina virtual**, insira ou selecione estas informações na página **Básico**:

   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Assinatura|Selecione sua assinatura.|
   |Resource group|Selecione **az-rg-1**.|
   |**Detalhes da instância**|
   |Nome da máquina virtual|Insira **vm-1**.|
   |Região|Selecione **(EUA) Leste dos EUA**.|
   |Opções de disponibilidade|No menu suspenso Zona de disponibilidade, selecione **Não é necessária redundância de infraestrutura.**|
   |Tipo de segurança|No menu suspenso Tipo de segurança, selecione **Standard.**|
   |Imagem|No menu suspenso Imagem, selecione **Datacenter do Windows Server 2022: Edição do Azure – x64 Gen2**.|
   |Arquitetura de VMs;|Deixe a configuração padrão como x64.|
   |Executar com desconto do Spot do Azure|Deixe a configuração padrão desmarcada.|
   |Tamanho|Deixe a configuração padrão como vcpus Standard_D2s_v3-2, 8 GiB de memória.|
   |**Conta de administrador**|
   |Nome de Usuário|Insira **Tenantadmin1**.|
   |Senha|Insira **Superuser#150**.|
   |Confirmar senha|Reinsira **Superuser#150.**|
   |**Regras de porta de entrada**|
   |Porta de entrada públicas|Selecione **Nenhum**.|
 
4. Selecione **Avançar: Discos** e **Avançar: Rede**.

5. Na página **Rede**, verifique ou insira as seguintes informações:

   |Configuração|Valor|
   |---|---|
   |**Interface de rede**|
   |Rede virtual|Selecione **vnet-1**.|
   |Sub-rede|Deixe a configuração padrão como sub-rede-1 (10.0.0.0/24).|
   |IP público|Deixe a configuração padrão como (novo) vm-1-ip.|
   |Grupo de segurança de rede da NIC|Selecione **Nenhum**.|
   
6. Selecione o botão **Revisar + criar** na parte inferior da página para prosseguir.

7. Selecione **Criar**. A implantação da VM pode levar alguns minutos.
  
   - Crie a segunda máquina virtual.

   - Repita as etapas anteriores para criar uma segunda máquina virtual chamada **vm-2**.

   - Aguarde a conclusão da implantação das VMs para avançar para a próxima seção.

### Associar interfaces de rede a um Grupo de Segurança de Aplicativos

>**Observação**: quando você criou as VMs, o Azure criou um adaptador de rede para cada VM e a anexou à VM. Adicione a interface de rede de cada VM para um dos grupos de segurança de aplicativos criados anteriormente:

1. Na caixa de pesquisa na parte superior do portal, insira **máquinas virtuais**. Selecione **Máquinas virtuais** nos resultados da pesquisa.

2. Selecione **vm-1**.
 
3. Escolha **Rede** na seção **vm-1**.

4. Escolha **Grupos de segurança do aplicativo** na seção **Rede** da **vm-1. Escolha **+ Adicionar grupos de segurança do aplicativo**

5. No modelo **Adicionar grupos de segurança do aplicativo**, escolha **asg-mgmt** no modelo **Grupos de segurança do aplicativo** e clique no botão **Adicionar** na parte inferior da página do modelo.

   ![imagem](https://github.com/user-attachments/assets/9bb38a91-8aa6-427b-9b6d-b01c5333ad4c)

7. Repita as etapas anteriores para **vm-2**, selecionando **asg-web** no modelo **Grupos de segurança do aplicativo**.

> **Resultados**: você criou uma infraestrutura de rede virtual e filtrou o tráfego de rede com um grupo de segurança de rede usando o portal do Azure.

> **Observação**: não remova os recursos deste laboratório, pois eles são necessários para os seguintes exercícios: Exercício 05 – Habilitar o acesso just-in-time em VMs, Exercício 06a – Configurar o Firewall e as Redes Virtuais do Key Vault.
