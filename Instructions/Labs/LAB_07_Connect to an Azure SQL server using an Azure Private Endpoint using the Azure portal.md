---
lab:
  title: Exercício 07 – Conectar-se a um servidor do SQL do Azure usando um Ponto de Extremidade Privado do Azure usando o portal do Azure
  module: Module 08 - Connect to an Azure SQL server using an Azure Private Endpoint using the Azure portal
---


>**Observação**: para concluir este laboratório, você precisará ter uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) na qual você tem acesso administrativo. 


Um ponto de extremidade privado do Azure é o bloco de construção básico para o Link Privado no Azure. Ele permite que recursos do Azure, como VMs (máquinas virtuais), se comuniquem de modo privado e seguro com recursos do Link Privado, como o SQL Server do Azure.

---

## Tarefas de habilidades

- Criar uma rede virtual e um bastion host.
  
- Crie uma máquina virtual.
  
- Criar um SQL Server do Azure e um ponto de extremidade privado.
  
- Testar a conectividade com o ponto de extremidade privado do SQL Server.

## Instruções para o exercício 

### Criar um grupo de recursos e uma rede virtual.

>**Observação**: O host bastion será usado para se conectar com segurança à máquina virtual para testar o ponto de extremidade privado. 

1. Abra uma sessão do navegador e entre no [menu do portal do Azure](https://portal.azure.com/).
   
2. Na caixa de pesquisa na parte superior do portal, digite **Redes virtuais**. Selecione **Redes virtuais** nos resultados da pesquisa.

3. Na página **Redes virtuais**, selecione **+ Criar**.

4. Na guia **Básico** em **Criar rede virtual**, insira ou selecione estas informações:
   
   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Selecione **az-rg-1**.|
   |**Detalhes da instância**|
   |Nome da rede virtual|Insira **vnet-2.**|
   |Região|Selecione **(EUA) Leste dos EUA**.|  
    
5. Selecione **Avançar** para prosseguir para a guia **Segurança**.
  
6. Selecione **Habilitar o Azure Bastion** na seção Azure Bastion da guia Segurança.

   >**Observação**: o Azure Bastion é um serviço pago que fornece conectividade de RDP/SSH segura às suas máquinas virtuais via TLS. Quando você se conecta usando o Azure Bastion, suas máquinas virtuais não precisam de um endereço IP público. 

7. Insira ou selecione as seguintes informações no campo **Azure Bastion**:

   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Host do Azure Bastion |Insira **az-bastionhost-1a.**|
   |Nome do endereço IP público do Azure Bastion|Selecione **Criar um endereço IP público**|
   |Adicionar um endereço IP público|Selecione **OK**|

9. Selecione **Avançar** para prosseguir para a guia **Endereços de IP**.

10. Na caixa de **espaço de endereço IPv4** configurada, na coluna **Sub-redes**, clique na entrada **padrão**.

11. No modelo **Editar sub-rede**, insira ou selecione as seguintes informações:

    |Configuração|Valor|
    |---|---|
    |**Detalhes do projeto**|
    |Finalidade da sub-rede|Deixe a configuração padrão como Padrão.|
    |Nome|**subnet-2**|
    |Intervalo de endereços IPv4|Deixe a configuração padrão como 10.0.0.0/16.|
    |Endereço inicial|Deixe a configuração padrão como /24 (256 endereços).|

13. Na parte inferior da página **Editar sub-rede**, clique em **Salvar**.

14. Na parte inferior da página **Endereços IP**, clique em **Revisar + criar**.

    >**Observação**: A implantação do Bastion pode levar até 15 minutos para a instanciação completa.

15. Na parte inferior da página **Revisar + criar** clique em **Criar**.
 
### Crie uma máquina virtual.

>**Observação**: nesta tarefa, você criará uma máquina virtual que será usada para testar o ponto de extremidade privado.

1. No portal, pesquise e selecione **Máquinas virtuais**.

2. Em **Máquinas virtuais**, selecione **+ Criar** e, em seguida, **Máquina virtual do Azure**.

3. Em Criar máquina virtual, insira ou selecione estas informações na página **Básico**:

   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Assinatura|Selecione sua assinatura.|
   |Resource group|Selecione **az-rg-1**.|
   |**Detalhes da instância**|
   |Nome da máquina virtual|Insira **vm-3.**|
   |Região|Selecione **(EUA) Leste dos EUA**.|
   |Opções de disponibilidade|No menu suspenso Zona de disponibilidade, selecione **Não é necessária redundância de infraestrutura.**|
   |Tipo de segurança|No menu suspenso Tipo de segurança, selecione **Standard.**|
   |Imagem|Selecione **Windows Server 2022 Datacenter – x64 Gen2**.|
   |Arquitetura de VMs;|Selecione **x64**.|
   |Executar com desconto do Spot do Azure|Deixe a configuração padrão desmarcada.|
   |Tamanho|Deixe a configuração padrão como vcpus Standard_D2s_v3-2, 8 GiB de memória.|
   |**Conta de administrador**|
   |Nome de Usuário|Insira **Tenantadmin2.**|
   |Senha|Insira **Superuser#170.**|
   |Confirmar senha|Reinsira **Superuser#170.**|
   |**Regras de porta de entrada**|
   |Selecione as portas de entrada|Selecione **Nenhum**.|

5. Selecione **Avançar: Discos** e **Avançar: Rede**.
  
6. Na página **Rede**, insira ou selecione estas informações:

   |Configuração|Valor|
   |---|---|
   |**Interface de rede**|
   |Rede virtual|Selecione **vnet-2**.|
   |Sub-rede|Selecione **subnet-2 (10.0.0.0/24).**|
   |IP público|Selecione **Nenhum**.|
   |Grupo de segurança de rede da NIC|Selecione **Básico**.|
   |Porta de entrada públicas|Selecione **Nenhum**.|
   |Selecione as portas de entrada|Deixe a configuração padrão como em branco.|
   |Excluir o adaptador de rede quando a VM é excluída|Deixe a configuração padrão como Habilitar rede acelerada marcada.|
   |Balanceamento de carga|Mantenha a configuração padrão como Nenhum.|
  
6. Selecione **Examinar + criar**.

7. Examine as configurações e selecione **Criar**.

### Criar um SQL Server do Azure e um ponto de extremidade privado

>**Observação**: nesta tarefa, você criará um SQL Server no Azure.

1. Na caixa de pesquisa na parte superior do portal, insira **banco de dados sql**. Selecione **Bancos de dados SQL** nos resultados da pesquisa.

2. Na página **Bancos de Dados SQL**, selecione **+ Criar**.
   
3. Na guia **Básico** de **Criar banco de dados SQL**, insira ou selecione estas informações:

   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Selecione **az-rg-1**.|
   |**Detalhes do banco de dados**|
   |Nome do banco de dados|Insira **az-sql-db1a.**|
   |Nome do servidor|Insira **az-sql-svr1a.** Se esse nome já estiver sendo usado, crie um nome exclusivo.|
   |Location|Selecione **(EUA) Leste dos EUA**.|
   |**Autenticação**|
   |Método de autenticação|Selecione **Usar a autenticação SQL**.|
   |Logon de administrador do servidor|Insira **Tenantadmin2.**|
   |Senha|Insira **Superuser#170.**|
   |Confirmar senha|Insira **Superuser#170.**|

4. Selecione **OK**.
   
   |Configuração|Valor|
   |---|---|
   |**Detalhes do banco de dados**|
   |Deseja usar o pool elástico SQL|Deixe a configuração padrão como Não.|
   |Ambiente de carga de trabalho|Deixe a configuração padrão como Desenvolvimento.|
   |Computação + armazenamento|Deixe a configuração padrão como Uso Geral - Sem Servidor.|
   |**Redundância do armazenamento de backup**|
   |Redundância do armazenamento de backup|Selecione **Armazenamento de backup com redundância local**.|
   
5. Selecione a guia **Rede** ou escolha o botão **Avançar: Rede**.

6. Na guia **Rede**, insira ou selecione estas informações:

   |Configuração|Valor|
   |---|---|
   |**Conectividade de rede**|
   |Método de conectividade|Selecione **Ponto de extremidade privado**.|
   |Política de Conexão|Deixe a configuração padrão como Padrão – Usa a política de redirecionamento para todas as conexões de cliente originadas no Azure (exceto conexões de ponto de extremidade privado) e no Proxy para todas as conexões de cliente originadas fora do Azure|
   |Conexões de criptografia|Deixe a configuração padrão como TLS.12|

7. Selecione **+ Adicionar ponto de extremidade privado** em **Pontos de extremidade privados**.

8. Em **Criar ponto de extremidade privado**, insira ou selecione estas informações:

   |Configuração|Valor|
   |---|---|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Selecione **az-rg-1**.|
   |Localidade|Selecione **Leste dos EUA**.|
   |Nome|Insira **az-pe-1a.**|
   |Sub-recurso de destino|Deixe a configuração padrão como SqlServer.|
   |**Rede**|
   |Rede virtual|Selecione **vnet-2**.|
   |Sub-rede|Selecione **subnet-2.**|
   |**Integração de DNS privado**|
   |Integrar com a zona de DNS privado|Deixe a configuração padrão como Sim.|
   |Zona DNS privado|Deixe a configuração padrão como (Novo) privatelink.database.windows.net.|

9. Selecione **OK**.

10. Selecione **Examinar + criar**.

11. Selecione **Criar**.

### Desabilitar o acesso público ao SQL Server lógico do Azure

>**Observação**: para esta tarefa, suponha que você gostaria de desabilitar todo o acesso público ao SQL Server do Azure e permitir apenas conexões a partir de sua rede virtual. O padrão da configuração **Acesso público** pode ser **Desativar**.

1. Na caixa de pesquisa portal do Azure, insira **az-sql-svr1a** ou o nome do servidor que você inseriu nas etapas anteriores.

2. Selecione **Rede** na seção **Segurança** de **az-sql-svr1a.** Na página **Rede**, selecione a guia **Acesso público** e, em seguida, selecione **Desabilitar** para **Acesso à rede pública**.

   ![imagem](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/44ff5c24-70cf-49ed-b2ab-5e210c478b3a)

3. Selecione **Salvar**.

### Testar a conectividade com o ponto de extremidade privado

>**Observação**: nesta tarefa, você usará a máquina virtual criada nas etapas anteriores para se conectar ao SQL Server pelo ponto de extremidade privado.

1. Selecione **Grupos de recursos** no painel de navegação à esquerda.

2. Selecione **az-rg-1**.

3. Selecione **vm-3.**

4. Na página de visão geral de **vm-3**, escolha Conectar e, em seguida, **Bastion**.

5. Insira o nome de usuário **Tenantadmin2** e a senha **Superuser#170** que você inseriu durante a criação da máquina virtual.

   **Importante:** vá para as configurações de Borda/Pop-ups e redirecionamentos/e alterne a opção Bloqueado para **desativado** antes de selecionar Conectar.

7. Selecione o botão **Conectar**.
  
8. Abra o Windows PowerShell no servidor depois de se conectar.

9. Insira `nslookup sqlserver-name.database.windows.net.` Substitua **sqlserver-name** pelo nome do SQL Server criado nas etapas anteriores. Você receberá uma mensagem semelhante à mostrada abaixo:

   ````  
   Server:  UnKnown
   Address:  168.63.129.16
   
   Non-authoritative answer:
   Name:    az-sql-svr1a.privatelink.database.windows.net
   Address:  10.1.0.5
   Aliases:  az-sql-svr1a.database.windows.net
   ````
    
>**Observação**: o endereço IP privado 10.1.0.5 é retornado para o nome do SQL Server. Esse endereço está na sub-rede **az-sql-svr1a** da rede virtual **vnet-2** criada anteriormente.

9. Instale o [SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&view=sql-server-2017) em **vm-3**.
 
10. Abra o **SQL Server Management Studio**.

11. Em **Conectar-se ao servidor**, insira ou selecione estas informações:

    |Configuração|Valor|
    |---|---|
    |Tipo de servidor|Selecione **Mecanismo de Banco de Dados**.|
    |Nome do servidor|Insira **az-sql-svr1a.database.windows.net.**|
    |Autenticação|Selecione **Autenticação do SQL Server**.|
    |Nome de usuário|Insira **Tenantadmin2**.|
    |Senha|Insira **Superuser#170**.|
    |Lembrar senha|Selecione **Sim**.|
    |Segurança da conexão|
    |Criptografia|Deixe a configuração padrão como Obrigatório.|
   
13. Selecione **Conectar**.

14. Procurar bancos de dados no menu à esquerda.

15. Feche a conexão da área de trabalho remota da vm-3.
  
> **Resultados**: você se conectou a um SQL Server do Azure por meio de um Ponto de Extremidade Privado do Azure usando o portal do Azure.
