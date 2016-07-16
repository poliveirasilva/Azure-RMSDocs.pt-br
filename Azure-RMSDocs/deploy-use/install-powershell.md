---
title: Instalando o Windows PowerShell para Azure Rights Management | Azure RMS
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
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 590148218fdd10e88ba764b2dc523a2213e2c8bb


---

# Instalando o Windows PowerShell para Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Use as seguintes informações para ajudar na instalação do Windows PowerShell para Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS).

Você pode usar este módulo do Windows PowerShell para administrar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] a partir da linha de comando usando qualquer computador que tenha uma conexão com a Internet e que atenda aos pré-requisitos listados na próxima seção. O Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] dá suporte para scripts para automação ou pode ser necessário para cenários de configuração avançada. Para obter mais informações sobre as tarefas e as configurações de administração aos quais o módulo dá suporte, consulte [Administração do Azure Rights Management usando o Windows PowerShell](administer-powershell.md).

## Pré-requisitos
Esta tabela lista os pré-requisitos para instalar e usar o Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

|Requisito|Mais informações|
|---------------|--------------------|
|A versão do Windows que suporta o módulo de administração do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]|Verifique a lista de sistemas operacionais que oferecem suporte na seção **Requisitos de Sistema** na [página de download para a Ferramenta de Administração do Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721).|
|Versão mínima do Windows PowerShell: 2.0|O suporte para o módulo de administração [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] foi introduzido no Windows PowerShell 2.0.<br /><br />Por padrão, a maioria dos sistemas operacionais Windows é instalada com pelo menos a versão 2.0 do Windows PowerShell. Se você precisar instalar o Windows PowerShell 2.0, consulte [Instalar o Windows PowerShell 2.0](http://msdn.microsoft.com/library/ff637750.aspx).<br /><br />Dica: você pode confirmar a versão do Windows PowerShell que está executando digitando **$PSVersionTable** em uma sessão do Windows PowerShell.|
|Versão mínima do Microsoft .NET Framework: 4.5<br /><br />Observação: essa versão do Microsoft .NET Framework está incluída nos sistemas operacionais mais recentes, portanto, você precisará realizar uma instalação manual somente se o sistema operacional cliente for anterior ao Windows 8.0 ou se o sistema operacional do servidor for anterior ao Windows Server 2012.|Se a versão mínima do Microsoft .NET Framework não estiver instalada, você poderá baixar o [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653).<br /><br />A versão mínima do Microsoft .NET Framework é necessária para algumas das classes que o módulo de administração [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] utiliza.|
|Assistente de Conexão do Microsoft Online Services 7.0|O Assistente de Conexão do Microsoft Online Services é necessário para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] autenticação.<br /><br />Para obter mais informações, consulte o [Centro de Download: Assistente do Microsoft Online Services para profissionais de TI RTW](http://www.microsoft.com/en-us/download/details.aspx?id=41950).|

## Como instalar o módulo de administração do Rights Management

1.  Vá para o Centro de Download da Microsoft e [baixe a Ferramenta de Administração do Azure Rights Management](https://go.microsoft.com/fwlink/?LinkId=257721)que contém o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] módulo de administração do Windows PowerShell.

2.  Na pasta local onde você baixou e salvou o arquivo de instalação do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], clique duas vezes no arquivo executável que baixou para a plataforma (WindowsAzureADRightsManagementAdministration_x64 ou WindowsAzureADRightsManagementAdministration_x86.exe) para iniciar o Assistente de configuração de administração de gerenciamento de direitos do AD do Azure.

3.  Conclua o assistente.

O Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] agora está instalado.

## Próximas etapas
Para ver quais cmdlets estão disponíveis, inicie o Windows PowerShell com a opção **Executar como administrador** e digite o seguinte:

```
Get-Command -Module aadrm
```
Use o comando `the Get-Help <cmdlet_name>` para ver a Ajuda de um cmdlet específico.

Para obter mais informações:

-   Lista completa de cmdlets disponíveis: [Cmdlets do Azure Rights Management](https://msdn.microsoft.com/library/windowsazure/dn629398.aspx)

-   Lista dos principais cenários de configuração que dão suporte para Windows PowerShell: [Administração do Azure Rights Management usando o Windows PowerShell](administer-powershell.md)

Antes de executar qualquer comando que configure o serviço [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], você deve conectar-se ao serviço usando o cmdlet [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx). Quando você terminar de executar os comandos de configuração que deseja, desconecte-se do serviço usando o cmdlet [Disconnect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629416.aspx) .

> [!NOTE]
> Se [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] ainda não foi ativado, você pode fazer isso depois de se conectar ao serviço usando o cmdlet [Enable-Aadrm](https://msdn.microsoft.com/library/windowsazure/dn629412.aspx).

## Consulte também
[Administrando o Azure Rights Management usando o Windows PowerShell](administer-powershell.md)



<!--HONumber=Jun16_HO4-->


