---
# required metadata

title: Instalar o Windows PowerShell para o Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalar o Windows PowerShell para o Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Utilize as seguintes informações para o ajudar a instalar o Windows PowerShell para o Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS).

Pode utilizar este módulo do Windows PowerShell para administrar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] na linha de comandos, utilizando qualquer computador que tenha uma ligação à Internet e que cumpra os pré-requisitos indicados na secção seguinte. O Windows PowerShell para o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] suporta o scripting para a automatização ou poderá ser necessário para cenários de configuração avançada. Para obter mais informações sobre as tarefas de administração e as configurações que o módulo suporta, consulte [Administrar o Azure Rights Management utilizando o Windows PowerShell](administer-powershell.md).

## Pré-requisitos
Esta tabela lista os pré-requisitos para instalar e utilizar o Windows PowerShell para o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

|Requisito|Mais informações|
|---------------|--------------------|
|Uma versão do Windows que suporte o módulo de administração do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]|Verifique a lista de sistemas operativos suportados na secção **Requisitos de Sistema** da [página de transferência da Ferramenta de Administração do Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721).|
|Versão mínima do Windows PowerShell: 2.0|O suporte para o módulo de administração do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] é apresentado no Windows PowerShell 2.0.<br /><br />Por predefinição, a maioria dos sistemas operativos do Windows instala com, pelo menos, a versão 2.0 do Windows PowerShell. Se precisar de instalar o Windows PowerShell 2.0, consulte [Instalar o Windows PowerShell 2.0](http://msdn.microsoft.com/library/ff637750.aspx).<br /><br />Dica: pode confirmar a versão do Windows PowerShell que está a executar, escrevendo **$PSVersionTable** numa sessão do Windows PowerShell.|
|Versão mínima do Microsoft .NET Framework: 4.5<br /><br />Nota: esta versão do Microsoft .NET Framework está incluída em sistemas operativos posteriores, pelo que apenas deve instalá-la manualmente se o sistema operativo cliente for inferior ao Windows 8.0 ou o sistema operativo do servidor for inferior ao Windows Server 2012.|Se a versão mínima do Microsoft .NET Framework não estiver já instalada, pode transferir o [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).<br /><br />Esta versão mínima do Microsoft .NET Framework é necessária para algumas das classes que o módulo de administração do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] utiliza.|
|Assistente de Início de Sessão no Microsoft Online Services 7.0|O Assistente de Início de Sessão no Microsoft Online Services é necessário para a autenticação do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].<br /><br />Para obter mais informações, consulte [Centro de Transferências: Assistente do Microsoft Online Services para Profissionais de TI RTW](http://www.microsoft.com/en-us/download/details.aspx?id=41950).|

## Como instalar o módulo de administração do Rights Management

1.  Aceda ao Centro de Transferências da Microsoft e [transfira a Ferramenta de Administração do Azure Rights Management](https://go.microsoft.com/fwlink/?LinkId=257721), que contém o módulo de administração do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para o Windows PowerShell.

2.  Na pasta local onde transferiu e guardou o ficheiro do instalador do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], faça duplo clique no ficheiro executável que transferiu para a plataforma (WindowsAzureADRightsManagementAdministration_x64 ou WindowsAzureADRightsManagementAdministration_x86.exe) para iniciar o Assistente de Configuração de Administração do Azure AD Rights Management.

3.  Conclua o assistente.

O Windows PowerShell para o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] está agora instalado.

## Passos seguintes
Para ver os cmdlets que estão disponíveis, inicie o Windows PowerShell com a opção **Executar como administrador** e escreva o seguinte:

```
Get-Command -Module aadrm
```
Utilize o comando `the Get-Help <cmdlet_name>` para ver a Ajuda para um cmdlet específico.

Para mais informações:

-   Lista completa dos cmdlets disponíveis: [Cmdlets do Azure Rights Management](https://msdn.microsoft.com/library/windowsazure/dn629398.aspx)

-   Lista dos principais cenários de configuração que suportam o Windows PowerShell: [Administrar o Azure Rights Management ao Utilizar o Windows PowerShell](administer-powershell.md)

Antes de poder executar quaisquer comandos para configurar o serviço [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], tem de ligar ao serviço através do cmdlet [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx). Quando terminar de executar os comandos de configuração que pretende, desligue do serviço através do cmdlet [Disconnect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629416.aspx).

> [!NOTE]
> Se ainda não ativou o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], pode fazê-lo depois de ligar ao serviço, utilizando o cmdlet [Enable-Aadrm](https://msdn.microsoft.com/library/windowsazure/dn629412.aspx).

## Consulte Também
[Administrar o Azure Rights Management ao Utilizar o Windows PowerShell](administer-powershell.md)


<!--HONumber=Apr16_HO4-->


