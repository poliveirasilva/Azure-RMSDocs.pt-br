---
# required metadata

title: Configurando os superusuários para o Azure Rights Management e os serviços de descoberta ou a recuperação de dados | Azure RMS
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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurando os superusuários para o Azure Rights Management e os serviços de descoberta ou a recuperação de dados

*Aplica-se a: Azure Rights Management, Office 365*

O recurso de superusuário do Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) garante que serviços e pessoas autorizadas sempre possam ler e inspecionar os dados que o Azure RMS protege para sua organização. E, se necessário, remover a proteção ou alterar a proteção aplicada anteriormente. Um superusuário sempre tem direitos totais de proprietário para todas as licenças de uso concedidas pelo locatário do RMS da organização. Essa capacidade às vezes é chamada de "raciocínio sobre dados" e é um elemento crucial para manter o controle dos dados da sua organização. Por exemplo, você usaria esse recurso para qualquer um dos seguintes cenários:

-   Um funcionário deixa a empresa e você precisa ler os arquivos protegidos.

-   Um administrador de TI precisa remover a política de proteção atual que foi configurada para arquivos e aplicar uma nova política de proteção.

-   O Exchange Server precisa indexar caixas de entrada de email para operações de pesquisa.

-   Você tem serviços de TI existentes para soluções de prevenção de perda de dados (DLP), gateways de criptografia do conteúdo (CEG) e produtos antimalware que precisam inspecionar arquivos que já estão protegidos.

-   É preciso descriptografar arquivos em massa por motivos de auditoria, legais ou outros motivos de conformidade.

Por padrão, o recurso de superusuário não está habilitado e nenhum usuário recebe essa função. Ele é habilitado para você automaticamente caso você configure o conector do Rights Management para o Exchange, e não é necessário para serviços padrão que executam o Exchange Online, o SharePoint Online ou o SharePoint Server.

Se você precisar habilitar o recurso de superusuário manualmente, use o cmdlet do Windows PowerShell [Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx) e atribua usuários (ou contas de serviço), conforme necessário, usando o cmdlet [Add-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629411.aspx) ou o cmdlet [Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx) e adicione usuários (ou outros grupos) a este grupo conforme necessário. 

> [!NOTE]
> Se você ainda não instalou o módulo do Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], consulte [Instalando o Windows PowerShell para Azure Rights Management](install-powershell.md).

Práticas recomendadas de segurança para o recurso de superusuário:

-   Restrinja e monitore os administradores que recebem um administrador global para seu locatário do Office 365 ou Azure RMS ou que recebem a função AdministradorGlobal usando o cmdlet [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629417.aspx) . Esses usuários podem habilitar o recurso de superusuário e atribuir usuários (e a si mesmos) como superusuários e potencialmente descriptografar todos os arquivos que protegem a sua organização.

-   Para ver quais usuários e contas de serviço são atribuídos individualmente como superusuários, use o [cmdlet Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx). Para ver se um grupo de superusuários está configurado, use o cmdlet [Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/mt653942.aspx) e suas ferramentas de gerenciamento de usuário padrão para verificar quais usuários são membros deste grupo. Como todas as ações de administração, as ações habilitar ou desabilitar o recurso de super e adicionar ou remover superusuários são registradas e podem ser auditadas usando o comando [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) . Quando os superusuários descriptografam arquivos, essa ação é registrada e pode ser auditada com [log de uso](log-analyze-usage.md).

-   Se o recurso de superusuário não for necessário para serviços diários, ative o recurso somente quando você precisar dele e desative-o novamente usando o cmdlet [Disable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629428.aspx) .

A extração de log a seguir mostra algumas entradas de exemplo do uso do cmdlet Get-AadrmAdminLog. Neste exemplo, o administrador da Contoso Ltd confirma que o recurso de superusuário está desabilitado, adiciona Richard Simone como um superusuário verifica se Richard é o único superusuário configurado para o Azure RMS e, em seguida, habilita o recurso de superusuário para que Richard agora possa descriptografar alguns arquivos que foram protegidos por um funcionário que agora saiu da empresa.

`2015-08-01T18:58:20    admin@contoso.com   GetSuperUserFeatureState    Passed  Disabled`

`2015-08-01T18:59:44    admin@contoso.com   AddSuperUser -id rsimone@contoso.com    Passed  True`

`2015-08-01T19:00:51    admin@contoso.com   GetSuperUser    Passed  rsimone@contoso.com`

`2015-08-01T19:01:45    admin@contoso.com   SetSuperUserFeatureState -state Enabled Passed  True`

## Opções de script para superusuários
Muitas vezes, alguém a quem é atribuído um superusuário para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] precisa remover a proteção de vários arquivos em vários locais. Embora seja possível fazer isso manualmente, é mais eficiente (e geralmente mais confiável) gerar um script disso. Para fazer isso, [baixar a Ferramenta de Proteção RMS](http://www.microsoft.com/en-us/download/details.aspx?id=47256). Em seguida, use o cmdlet [Unprotect-RMSFile](https://msdn.microsoft.com/library/azure/mt433200.aspx) e o cmdlet [Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx), conforme necessário.

Para obter mais informações sobre esses cmdlets, consulte [Cmdlets de proteção do RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).

> [!NOTE]
> O módulo RMSProtection PowerShell, que acompanha a Ferramenta de Proteção RMS, é diferente e complementa o principal [módulo do Windows PowerShell para Azure Rights Management](administer-powershell.md). O módulo de Proteção por RMS dá suporte a ambos o Azure RMS e o AD RMS.




<!--HONumber=Apr16_HO4-->


