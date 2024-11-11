---
lab:
  title: 'Exercício 05: Habilitar o acesso just-in-time em VMs'
  module: Module 06 - Explore just-in-time VM access
---


>**Observação**: para concluir este laboratório, você precisará ter uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) na qual você tem acesso administrativo. 


Você pode usar o acesso JIT (just-in-time) do Microsoft Defender para Nuvem a fim de proteger suas VMs (máquinas virtuais) do Azure contra o acesso não autorizado à rede. Muitas vezes, os firewalls contêm regras de permissão que deixam suas VMs vulneráveis a ataques. O JIT permite que você autorize o acesso às suas VMs somente quando ele for necessário, nas portas necessárias e pelo período de tempo necessário. 

---

## Tarefas de habilidades

- Habilitar o JIT em suas VMs pelo portal do Azure.

- Solicitar acesso a uma VM que tenha o JIT habilitado pelo portal do Azure.

## Instruções para o exercício 

### Habilitar o JIT em suas VMs de máquinas virtuais do Azure

>**Observação**: você pode habilitar o JIT em uma VM nas páginas de máquinas virtuais do Azure do portal do Azure.

1. Abra uma sessão do navegador e faça logon no [menu do portal do Azure](https://portal.azure.com/).
  
2. Na caixa de pesquisa na parte superior do portal, insira **máquinas virtuais**. Selecione **Máquinas virtuais** nos resultados da pesquisa.

3. Selecione **vm-1**.
 
4. Escolha **Configuração** na seção **Configurações** de vm-1.
   
5. Em **Acesso à VM Just-In-Time** selecione **Habilitar Just-In-Time**.

6. Em **Acesso à VM just-in-time,** clique no link que diz **Abrir Microsoft Defender para Nuvem.**

7. Por padrão, o acesso just-in-time para a VM usa estas configurações:

   - Máquinas do Windows
   
     - Porta RDP: 3389
     - Acesso máximo permitido: três horas
     - Endereços IP de origem permitidos: todos

   - Máquinas do Linux
     - Porta SSH: 22
     - Acesso máximo permitido: três horas
     - Endereços IP de origem permitidos: todos
   
8. Por padrão, o acesso just-in-time para a VM usa estas configurações:

   - Na guia **configurada**, clique com o botão direito do mouse na VM à qual você deseja adicionar uma porta e selecione Editar.

   ![imagem](https://github.com/user-attachments/assets/aa4ded55-c5b1-4d40-b5a0-a4c33b9eb81b)
   
   - Em **Configuração de acesso JIT à VM**, você pode editar as configurações existentes de uma porta já protegida ou pode adicionar uma nova porta personalizada.
   - Ao terminar de editar as portas, selecione **Salvar**.   

### Solicitar acesso a uma VM habilitada para JIT na página conectar da máquina virtual do Azure.

>**Observação**: quando uma VM tem um JIT habilitado, você precisa solicitar acesso para se conectar a ele. Você pode solicitar acesso em qualquer uma das maneiras com suporte, independentemente de como você habilitou o JIT.
   
1. No portal do Azure, abra a página de máquinas virtuais.

2. Selecione a VM à qual você deseja se conectar e abra a página **conectar**.

   - O Azure verifica se o JIT está habilitado nessa VM.

        - Se o JIT não estiver habilitado para a VM, você será solicitado a habilitá-lo.
    
        - Se o JIT estiver habilitado, selecione **Solicitar acesso** para passar uma solicitação de acesso com o IP solicitante, o intervalo de tempo e as portas que foram configuradas para essa VM.
    
   ![imagem](https://github.com/user-attachments/assets/f5d0b67c-7731-4261-b0eb-a56c505dadd4)

> **Resultados**: você explorou vários métodos sobre como habilitar o JIT em suas VMs e como solicitar acesso a VMs que têm o JIT habilitado no Microsoft Defender para Nuvem.
