---
lab:
  title: Exercício 06 – Implantar uma máquina virtual para testar a conectividade de forma privada e segura com o SQL Server no ponto de extremidade privado
  module: Module 06 - Connect to an Azure SQL server using an Azure Private Endpoint using the Azure portal
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

>****: o bastion host será usado para se conectar com segurança à máquina virtual para testar o ponto de extremidade privado.

1. Abra uma sessão do navegador e entre no [menu do portal do Azure](https://portal.azure.com/).
   
2. No menu do portal do Azure, selecione + **Criar um recurso** > **Rede** > **Rede Virtual** ou pesquise Rede Virtual na caixa de pesquisa do portal.

3. Selecione **Criar**.

4. Na guia **Básico** em **Criar rede virtual**, insira ou selecione estas informações:
   
   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Selecione **Criar novo**. Insira **CreateSQLEndpointTutorial.** Selecione **OK**|
   |**Detalhes da instância**|
   |Nome da rede virtual|Insira **myVNet1a.**|
   |Region|Selecione **Leste dos EUA**.|  
    
5. Selecione a guia **Endereços IP** ou selecione o botão **Avançar: Endereços IP** na parte inferior da página.

6. Na guia **Endereços IP**, insira estas informações:

   |Configuração|Valor|
   |---|---|
   |Espaço de endereço IPv4|Insira **10.1.0.0/16**.|

7. Em **Nome da sub-rede**, selecione a palavra **padrão**.

8. Em **Editar sub-rede**, insira estas informações:

   |Configuração|Valor|
   |---|---|
   |Nome da sub-rede|Insira **mySubnet1a.**|
   |Intervalo de endereços da sub-rede|Insira **10.1.0.0/24**.|

9. Selecione **Salvar**.

10. Selecione a guia **Segurança**.

11. Em **Bastion host**, selecione **Habilitar**. Insira estas informações:
    
    |Configuração|Valor|
    |---|---|
    |Nome do bastion|Insira **myBastionHost**.|
    |Espaço de endereço da AzureBstionSubnet|Insira **10.1.1.0/24**.|
    |Endereço IP público|Selecione **Criar novo**. Em **Nome**, insira **My BastionIP.** Selecione **OK**.| 
 
### Crie uma máquina virtual.

>**Observação**: nesta tarefa, você criará uma máquina virtual que será usada para testar o ponto de extremidade privado.

1. No menu do portal do Azure, selecione + **Criar um recurso** > **Computação** > **Máquina virtual** ou procure **Máquina virtual** na caixa de pesquisa do portal.
   
2. Em **Criar uma máquina virtual**, insira ou selecione os valores na guia **Informações básicas**:

   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Assinatura|Selecionar sua assinatura|
   |Resource group|Selecione **CreateSQLEndpointTutorial**.|
   |**Detalhes da instância**|
   |Nome da máquina virtual|Insira a opção **myVM**.|
   |Região|Selecione **(EUA) Leste dos EUA**.|
   |Opções de disponibilidade|Deixe o padrão **Nenhuma redundância de infraestrutura necessária**.|
   |Tipo de segurança|Deixe o padrão de **Standard**.|
   |Imagem|Selecione **Windows Server 2022 Datacenter – x64 Gen2**.|
   |Arquitetura de VMs;|Selecione **x64**.|
   |Executar com desconto do Spot do Azure|Deixe o padrão de desmarcado|
   |Tamanho|Deixe o padrão de **Standard_D2s_v3-2 vcpus, 8 GiB de memória.**|
   |**Conta de administrador**|
   |Tipo de autenticação|Selecione **Senha**.|
   |Nome de Usuário|Insira **Tenantadmin2.**|
   |Senha|Insira **Superuser#170.**|
   |Confirmar senha|Reinsira **Superuser#170.**|
   |**Regras de porta de entrada**|
   |Selecione as portas de entrada|Selecione **Nenhum**.|

4. Selecione a guia **Rede** ou selecione **Avançar: Discos**, em seguida, **Avançar: Rede**.
  
5. Na guia **Rede**, insira ou selecione estas informações:

   |Configuração|Valor|
   |---|---|
   |**Interface de rede**|
   |Rede virtual|Selecione **myVNet1a.**|
   |Sub-rede|Selecione **mySubnet1a.**|
   |IP público|Selecione **Nenhum**.|
   |Grupo de segurança de rede da NIC|Selecione **Básico**.|
   |Porta de entrada públicas|Selecione **Nenhum**.|
  
6. Selecione **Examinar + criar**.

7. Examine as configurações e selecione **Criar**.

### Criar um SQL Server do Azure e um ponto de extremidade privado

>**Observação**: nesta tarefa, você criará um SQL Server no Azure.

1. No menu do portal do Azure, selecione + **Criar um recurso** > **Bancos de dados** > **Banco de dados SQL.**
   
2. Na guia **Básico** de **Criar banco de dados SQL**, insira ou selecione estas informações:

   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Selecione **CreateSQLEndpointTutorial**.|
   |**Detalhes do banco de dados**|
   |Nome do banco de dados|Insira **mysqldatabase**.|
   |Servidor|Selecione **Criar novo**.|  

3. Em **Criar Servidor de Banco de Dados SQL**, insira ou selecione estas informações:
  
   |Configuração|Valor|
   |---|---|
   |**Detalhes do servidor**|
   |Nome do servidor|Insira **mysqlserver1a.** Se esse nome já estiver sendo usado, crie um nome exclusivo.|
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
   |Deseja usar o pool elástico SQL|Selecione **Não**.|
   |Computação + armazenamento|Execute as configurações padrão ou selecione **Configurar banco de dados** para definir configurações de computação e de armazenamento.|
   |**Redundância do armazenamento de backup**|
   |Redundância do armazenamento de backup|Selecione **Armazenamento de backup com redundância local**.|
   
5. Selecione a guia **Rede** ou escolha o botão **Avançar: Rede**.

6. Na guia **Rede**, insira ou selecione estas informações:

   |Configuração|Valor|
   |---|---|
   |**Conectividade de rede**|
   |Método de conectividade|Selecione **Ponto de extremidade privado**.|

7. Selecione **+ Adicionar ponto de extremidade privado** em **Pontos de extremidade privados**.

8. Em **Criar ponto de extremidade privado**, insira ou selecione estas informações:

   |Configuração|Valor|
   |---|---|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Selecione **CreateSQLEndpointTutorial**.|
   |Location|Selecione **Leste dos EUA**.|
   |Nome|Insira **myPrivateSQLendpoint**.|
   |Sub-recurso de destino|Selecione **mysqlserver1a.**|
   |**Rede**|
   |Rede virtual|Selecione **myVNet1a.**|
   |Sub-rede|Selecione **mySubnet1a.**|
   |**Integração de DNS privado**|
   |Integrar com a zona de DNS privado|Mantenha o padrão **Sim**.|
   |Zona DNS privado|Mantenha o padrão **(Novo) privatelink.database.windows.net**.|

 9. Selecione **OK**.

 10. Selecione **Examinar + criar**.

 11. Selecione **Criar**.

### Desabilitar o acesso público ao SQL Server lógico do Azure

>**Observação**: para esta tarefa, suponha que você gostaria de desabilitar todo o acesso público ao SQL Server do Azure e permitir apenas conexões a partir de sua rede virtual.

1. Na caixa de pesquisa portal do Azure, insira **mysqlserver** ou o nome do servidor que você inseriu nas etapas anteriores.

2. Na página **Rede**, selecione a guia **Acesso público** e, em seguida, selecione **Desabilitar** para **Acesso à rede pública**.

   ![imagem](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/44ff5c24-70cf-49ed-b2ab-5e210c478b3a)


4. Selecione **Salvar**.

### Testar a conectividade com o ponto de extremidade privado

>**Observação**: nesta tarefa, você usará a máquina virtual criada nas etapas anteriores para se conectar ao SQL Server pelo ponto de extremidade privado.

1. Selecione **Grupos de recursos** no painel de navegação à esquerda.

2. Selecione **CreateSQLEndpointTutorial**.

3. Selecione **myVM**.

4. Na página de visão geral de **myVM**, selecione Conectar e **Bastion**.

5. Insira o nome de usuário **Tenantadmin2** e a senha **Superuser#170** que você inseriu durante a criação da máquina virtual.

   **Importante:** vá para as configurações de Borda/Pop-ups e redirecionamentos/e alterne a opção Bloqueado para **desativado** antes de selecionar Conectar.

7. Selecione o botão **Conectar**.
  
8. Abra o Windows PowerShell no servidor depois de se conectar.

9. Insira `nslookup sqlserver-name.database.windows.net.` Substitua **sqlserver-name** pelo nome do SQL Server criado nas etapas anteriores. Você receberá uma mensagem semelhante à mostrada abaixo:

   ````  
   Server:  UnKnown
   Address:  168.63.129.16
   
   Non-authoritative answer:
   Name:    mysqlserver1a.privatelink.database.windows.net
   Address:  10.1.0.5
   Aliases:  mysqlserver1a.database.windows.net
   ````
    
>**Observação**: o endereço IP privado 10.1.0.5 é retornado para o nome do SQL Server. Esse endereço está na sub-rede **mySubnet1a** da rede virtual **myVNet1a** criada anteriormente.

9. Instale o [SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&view=sql-server-2017) em **myVM**.
 
10. Abra o **SQL Server Management Studio**.

11. Em **Conectar-se ao servidor**, insira ou selecione estas informações:

    |Configuração|Valor|
    |---|---|
    |Tipo de servidor|Selecione **Mecanismo de Banco de Dados**.|
    |Nome do servidor|Insira **sqlserver1a.database.windows.net.**|
    |Autenticação|Selecione **Autenticação do SQL Server**.|
    |Nome de usuário|Insira **Tenantadmin2**.|
    |Senha|Insira **Superuser#170**.|
    |Lembrar senha|Selecione **Sim**.|
   
12. Selecione **Conectar**.

13. Procurar bancos de dados no menu à esquerda.

14. (Opcional) Crie ou consulte informações em mysqldatabase.

15. Feche a Conexão da Área de Trabalho Remota com myVM.
  
> **Resultados**: você se conectou a um SQL Server do Azure por meio de um Ponto de Extremidade Privado do Azure usando o portal do Azure.
