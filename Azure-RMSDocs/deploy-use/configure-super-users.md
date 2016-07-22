---
title: "Configurar superutilizadores para o Azure Rights Management e serviços de deteção ou recuperação de dados | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: acb4c00b-d3a9-4d74-94fe-91eeb481f7e3
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 0ca9b8d9643f5489c100fa3aa614e89cd396df52


---

# Configurar superutilizadores para o Azure Rights Management e serviços de deteção ou recuperação de dados

*Aplica-se a: Azure Rights Management, Office 365*

A funcionalidade de superutilizador do Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) assegura que as pessoas e os serviços autorizados podem sempre ler e inspecionar os dados que o Azure RMS protege na sua organização. E, se for necessário, remove a proteção ou altera a proteção que estava anteriormente aplicada. Um superutilizador tem sempre direitos de proprietário completos para todas as licenças de utilização que foram atribuídas pelo inquilino de RMS da organização. Esta capacidade é por vezes referida como “raciocínio através de dados” e é um elemento fundamental na manutenção do controlo dos dados da sua organização. Por exemplo, utilizaria esta funcionalidade para qualquer um dos seguintes cenários:

-   Um funcionário sai da organização e precisa de ler os ficheiros que ele protegeu.

-   Um administrador de TI tem de remover a política de proteção atual que foi configurada para OS ficheiros e aplicar uma nova política de proteção.

-   O Exchange Server necessita de indexar caixas de correio para operações de pesquisa.

-   Possui serviços de TI existentes para soluções de prevenção de perda de dados (DLP), gateways de encriptação de conteúdo (CEG) e produtos de antimalware que necessitam de inspecionar ficheiros que já estão protegidos.

-   É necessário desencriptar em volume ficheiros por motivos de auditoria, jurídicos ou outros motivos de conformidade.

Por predefinição, a funcionalidade de superutilizador não está ativada. Esta função não é atribuída a nenhum utilizador. É automaticamente ativado para si se configurar o conector Rights Management para Exchange e não é necessário para serviços padrão que executem o Exchange Online, o SharePoint Online ou o SharePoint Server.

Se precisar de ativar manualmente a funcionalidade de superutilizador, utilize o cmdlet do Windows PowerShell [Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx) e atribua utilizadores (ou contas de serviço), conforme necessário, ao utilizar o cmdlet [Add-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629411.aspx) ou o cmdlet [Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx) e adicione utilizadores (ou outros grupos), conforme necessário, a este grupo. 

> [!NOTE]
> Se ainda não tiver instalado o módulo do Windows PowerShell para o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], consulte [Instalar o Windows PowerShell para o Azure Rights Management](install-powershell.md).

Melhores práticas de segurança para a funcionalidade de superutilizador:

-   Restrinja e monitorize os administradores a quem é atribuída a função de administrador global para o seu inquilino do Office 365 ou do Azure RMS ou a quem é atribuída a função GlobalAdministrator ao utilizar o cmdlet [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx). Estes utilizadores podem ativar a funcionalidade de superutilizador e atribuir utilizadores (e os próprios) como superutilizadores, bem como desencriptar potencialmente todos os ficheiros que a sua organização protege.

-   Para ver quais os utilizadores e as contas de serviço que são atribuídos individualmente como superutilizadores, utilize o cmdlet [Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx). Para ver se um grupo de superutilizadores está configurado, utilize o cmdlet [Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/mt653942.aspx) e as suas ferramentas padrão de gestão de utilizadores para verificar quais os utilizadores que são membros deste grupo. Como todas as ações de administração, ativar ou desativar a funcionalidade super e adicionar ou remover superutilizadores, são registadas e podem ser auditadas ao utilizar o comando [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx). Quando os superutilizadores desencriptam ficheiros, esta ação é registada e pode ser auditada com o [registo de utilização](log-analyze-usage.md).

-   Se não necessitar da funcionalidade de superutilizador para os serviços diários, ative a funcionalidade apenas quando precisar dela e desative-a novamente ao utilizar o cmdlet [Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx).

O seguinte extrato de registo mostra algumas entradas de exemplo ao utilizar o cmdlet Get-AadrmAdminLog. Neste exemplo, o administrador da Contoso Ltd confirma que a funcionalidade de superutilizador está desativada, adiciona Guilherme Sarmento como um superutilizador, verifica se o Guilherme é o único superutilizador configurado para o Azure RMS e, em seguida, ativa a funcionalidade de superutilizador para que o Guilherme já possa desencriptar alguns ficheiros que foram protegidos por um empregado que tenha saído da empresa.

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## Opções de scripting para superutilizadores
É frequente que uma pessoa a quem seja atribuído um superutilizador para o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] venha a ter de remover a proteção de vários ficheiros, em várias localizações. Embora seja possível fazê-lo manualmente, é mais eficaz (e, muitas vezes, mais fiável) efetuar um script disto. Para tal, [transfira a Ferramenta de Proteção RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256). Em seguida, utilize o cmdlet [Unprotect-RMSFile](https://msdn.microsoft.com/library/azure/mt433200.aspx) e o cmdlet [Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx), conforme necessário.

Para obter mais informações acerca destes cmdlets, consulte [Cmdlets da Proteção RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).

> [!NOTE]
> O módulo do PowerShell de Proteção RMS que é fornecido com a Ferramenta de Proteção RMS é diferente do principal [módulo do Windows PowerShell para o Azure Rights Management](administer-powershell.md) e complementa-o. O módulo de Proteção RMS suporta o Azure RMS e o AD RMS.





<!--HONumber=Jun16_HO4-->


