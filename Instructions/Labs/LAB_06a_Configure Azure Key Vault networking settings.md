---
lab:
  title: Exercício 06a – Definir as configurações de rede do Azure Key Vault
  module: Module 07 - Configure Azure Key Vault networking settings
---


>**Observação**: para concluir este laboratório, você precisará ter uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) na qual você tem acesso administrativo. 


Você pode usar o portal do Azure para definir as configurações de rede do Azure Key Vault para trabalhar com outros aplicativos e serviços do Azure. 

---

## Tarefas de habilidades

- Crie um key vault usando o portal do Azure.

- Adicione uma rede virtual existente a um firewall e regras de rede virtual.

- Configure uma rede virtual e uma sub-rede para permitir o acesso a um cofre de chaves.

## Instruções para o exercício 

### Usar o portal do Azure para criar um Azure Key Vault.

1. Abra uma sessão do navegador e entre no [menu do portal do Azure](https://portal.azure.com/).
  
2. Na caixa de pesquisa, na parte superior do portal, insira **cofres de chaves**. Selecione **Cofres de chaves** nos resultados da pesquisa.

3. Na lista de resultados, escolha **Cofres de chaves**.

4. Na seção cofres de chaves, escolha **Criar.**

5. Na guia **Noções básicas** de **Criar um cofre de chaves**, insira ou selecione estas informações:
   
   |Configuração|Valor|
   |---|---|
   |**Detalhes do projeto**|
   |Subscription|Selecione sua assinatura.|
   |Resource group|Insira **az-rg-1.**|
   |**Detalhes da instância**|
   |Nome do cofre de chaves|O nome do cofre precisa conter apenas caracteres alfanuméricos e traços e não pode começar com um número. *Exemplo: az-securevault150*|
   |Region|Selecione **Leste dos EUA**.|
   |Tipo de preços|Deixe a configuração padrão como Padrão.|
   |Dias de retenção dos cofres excluídos|Deixe a configuração padrão como 90.|

6. Selecione a guia **Revisar + criar** ou selecione o botão azul Revisar + criar na parte inferior da página.
  
7. Selecione **Criar**.

### Definir as configurações do firewall e de rede virtual do Key Vault.

1. Na caixa de pesquisa do portal do Azure, insira **cofres de chaves**.

2. Navegue até o cofre de chaves criado anteriormente.

3. Clique em **Configurações**, **Rede** e na guia **Firewalls e redes virtuais**.
   
4. Em Permitir acesso de, selecione **Permitir acesso público de redes virtuais e endereços IP específicos.**

5. Na seção Redes virtuais, selecione + **Adicionar uma rede virtual** e, em seguida, selecione + **Adicionar redes virtuais existentes.**

6. No modelo **Adicionar redes**, selecione sua rede virtual criada anteriormente na lista suspensa **Redes virtuais** e na lista suspensa **Sub-redes**.

7. Na parte inferior do modelo **Adicionar redes**, clique em **Habilitar** e depois em **Adicionar**. 

8. Na parte inferior da página **Firewalls e redes virtuais**, clique em **Aplicar**.

  > **Resultados**: você criou um cofre de chaves e definiu as configurações de firewall e de rede virtual do cofre de chaves no portal do Azure.
