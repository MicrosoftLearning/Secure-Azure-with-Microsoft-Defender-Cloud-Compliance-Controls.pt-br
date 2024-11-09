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
   |Host do Azure Bastion |Insira **az-bastionhost-1a.**|
   |Nome do endereço IP público do Azure Bastion|Selecione **Criar um endereço IP público**|
   |Adicionar um endereço IP público|Selecione **OK**|

8. Selecione **Avançar** para prosseguir para a guia **Endereços de IP**.

9. Na caixa de **espaço de endereço IPv4** configurada, na coluna **Sub-redes**, clique na entrada **padrão**.

10. No modelo **Editar sub-rede**, insira ou selecione as seguintes informações:

    |Configuração|Valor|
    |---|---|
    |Finalidade da sub-rede|Deixe a configuração padrão como Padrão.|
    |Nome|**subnet-2**|
    |Incluir um espaço de endereço IPv4|Deixe a configuração padrão com a marca de seleção.|
    |Intervalo de endereços IPv4|Deixe a configuração padrão como 10.0.0.0/16.|
    |Endereço inicial|10.0.0.0.|
    |Tamanho|Deixe a configuração padrão como /24 (256 endereços).|
    |Intervalo de endereços da sub-rede|10.0.0.0-10.0.0.255.|

11. Na parte inferior da página **Editar sub-rede**, clique em **Salvar**.

12. Na parte inferior da página **Endereços IP**, clique em **Revisar + criar**.

13. Na parte inferior da página **Revisar + criar** clique em **Criar**.

>**Observação**: A implantação do Bastion pode levar até 15 minutos para a instanciação completa.
 
### Crie uma máquina virtual.

>**Observação**: nesta tarefa, você criará uma máquina virtual que será usada para testar o ponto de extremidade privado.

1. No portal, pesquise e selecione **Máquinas virtuais**.

2. Em **Máquinas virtuais**, selecione **+ Criar** e, em seguida, **Máquina virtual do Azure**.

3. Em Criar máquina virtual, insira ou selecione estas informações na página **Básico**:

   |Configuração|Valor|
   |---|---|
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
   |Porta de entrada públicas|Selecione **Nenhum**.|
   |Selecione as portas de entrada|A configuração padrão está esmaecida.|

4. Selecione **Avançar: Discos** e **Avançar: Rede**.
  
5. Na página **Rede**, insira ou selecione estas informações:

   |Configuração|Valor|
   |---|---|
   |**Interface de rede**|
   |Rede virtual|Selecione **vnet-2**.|
   |Sub-rede|Selecione **subnet-2 (10.0.0.0/24).**|
   |IP público|Selecione **Nenhum**.|
   |Grupo de segurança de rede da NIC|Selecione **Básico**.|
   |Porta de entrada públicas|Selecione **Nenhum**.|
   |Selecione as portas de entrada|A configuração padrão está esmaecida.|
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
   |Subscription|Selecione sua assinatura.|
   |Resource group|Selecione **az-rg-1**.|
   |**Detalhes do banco de dados**|
   |Nome do banco de dados|Insira **az-sql-db1a.**|
   |Servidor|Selecione **Criar novo**.|
   |**Detalhes do servidor**|
   |Nome do servidor|Insira **az-sql-srv1a**.|
   |Localidade|Deixe a configuração padrão como (EUA) Leste dos EUA|
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

7. Na seção **Pontos de extremidade privados**, selecione **+ Adicionar ponto de extremidade privado**.

8. Selecione **Examinar + criar**.

9. Selecione **Criar**.

10. Em **Criar ponto de extremidade privado**, insira ou selecione estas informações:

   |Configuração|Valor|
   |---|---|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Selecione **az-rg-1**.|
   |Localidade|Selecione **Leste dos EUA**.|
   |Nome|Insira **az-pe1a.**|
   |Sub-recurso de destino|Deixe a configuração padrão como SqlServer.|
   |**Rede**|
   |Rede virtual|Selecione **vnet-2**.|
   |Sub-rede|Selecione **subnet-2.**|
   |**Integração de DNS privado**|
   |Integrar com a zona de DNS privado|Deixe a configuração padrão como Sim.|
   |Zona DNS privado|Deixe a configuração padrão como (Novo) privatelink.database.windows.net.|

11. Selecione **OK**.

12. Selecione **Examinar + criar**.

13. Selecione **Criar**.

>**Observação**: a implantação do servidor do SQL do Azure e do ponto de extremidade privado pode levar até dez minutos para a instanciação completa.

### Permita que determinados endereços IP da Internet pública acessem seu servidor lógico do SQL do Azure.

>**Observação**: para esta tarefa, suponha que você gostaria de habilitar o acesso público ao servidor do SQL do Azure e permitir apenas conexões a partir de sua rede virtual. O padrão da configuração Acesso público pode ser **Desativado**.

1. Na caixa de pesquisa do portal do Azure, insira **az-sql-svr1a** ou o nome do servidor que você inseriu nas etapas anteriores.
   
2. Selecione **Rede** na seção **Segurança** de **az-sql-srv1a**.
  
3. Na página **Rede**, vá para a guia **Acesso público**.
  
4. Confirme se o **Acesso à rede pública** está desabilitado. Se não estiver, clique em **Redes selecionadas** em Acesso à rede pública.

>**Observação**: as conexões dos endereços IP configuradas na seção Regras de firewall abaixo terão acesso a este banco de dados. Por padrão, nenhum endereço IP público é permitido.

5. Se necessário, vá para a seção **Regras de firewall** na página **Rede** e selecione **+ Adicionar o endereço IPv4 do cliente** se o endereço IP do cliente ainda não estiver preenchido nos campos **Nome da regra**,**Endereço IPv4 inicial** e **Endereço IPv4 final**.
    
     ![imagem](https://github.com/user-attachments/assets/dfdeffca-d33f-44e1-81db-9f68a51f89df)

6. Se necessário, clique em **Salvar**.

### Testar a conectividade com o ponto de extremidade privado

>**Observação**: nesta tarefa, você usará a máquina virtual criada nas etapas anteriores para se conectar ao SQL Server pelo ponto de extremidade privado.

1. Na caixa de pesquisa do portal do Azure, digite **vm-3** e selecione-o na lista suspensa Recursos.

2. Na página **Visão geral** de vm-3, selecione **Conectar** e, em seguida, escolha **Bastion**.

3. Insira o nome de usuário **Tenantadmin2** e a senha **Superuser#170** que você inseriu durante a criação da máquina virtual.

   **Importante:** vá para as configurações de Borda/Pop-ups e redirecionamentos/e alterne a opção Bloqueado para **desativado** antes de selecionar Conectar.

4. Selecione o botão **Conectar**.
  
5. Abra o Windows PowerShell no servidor depois de se conectar.

6. Substitua **sqlserver-name** pelo nome do SQL Server criado nas etapas anteriores. Por exemplo, insira **nslookup az-sql-srv1a.database.windows.net**. Você receberá uma mensagem semelhante à mostrada abaixo:

   ````
   
   Server:  UnKnown
   Address:  168.63.129.16
   
   Non-authoritative answer:
   Name:    az-sql-srv1a.privatelink.database.windows.net
   Address:  10.1.0.5
   Aliases:  az-sql-srv1a.database.windows.net
   ````
   
>**Observação**: o endereço IP privado 10.1.0.5 é retornado para o nome do SQL Server. Esse endereço está na sub-rede **az-sql-srv1a** da rede virtual **vnet-2** criada anteriormente.

7. Instale o [SSMS (SQL Server Management Studio)](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&amp;view=sql-server-2017) em **vm-3**.
 
8. Abra o **SQL Server Management Studio**.

9. Em **Conectar-se ao servidor**, insira ou selecione estas informações:

    |Configuração|Valor|
    |---|---|
    |Tipo de servidor|Selecione **Mecanismo de Banco de Dados**.|
    |Nome do servidor|Insira **az-sql-srv1a.database.windows.net**.|
    |Autenticação|Selecione **Autenticação do SQL Server**.|
    |Nome de usuário|Insira **Tenantadmin2**.|
    |Senha|Insira **Superuser#170**.|
    |Lembrar senha|Selecione **Sim**.|
    |Segurança da conexão|
    |Criptografia|Deixe a configuração padrão como Obrigatório.|
   
10. Selecione **Conectar**.

11. Procurar bancos de dados no menu à esquerda.

12. Feche a conexão da área de trabalho remota da vm-3.
  
> **Resultados**: você se conectou a um SQL Server do Azure por meio de um Ponto de Extremidade Privado do Azure usando o portal do Azure.
