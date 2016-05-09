---
# required metadata

title: Administrando o Azure Rights Management usando o Windows PowerShell | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a890e04a-4b70-41b5-8d5f-3c210a669faa

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Administrando o Azure Rights Management usando o Windows PowerShell
Embora seja possível ativar o Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) usando o [!INCLUDE[o365_2](../includes/o365_2_md.md)] centro de administração do Portal clássico do Azure, você também pode usar o módulo Windows PowerShell para [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (AADRM) para fazer isso.

Após ativar o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], talvez não seja necessário ter uma administração adicional para o serviço. No entanto, alguns cenários de configuração avançados podem exigir o uso do módulo Windows PowerShell para o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]. A tabela a seguir lista alguns dos cenários de configuração avançada que usam o Windows PowerShell. Para obter uma lista completa dos cmdlets disponíveis com mais informações sobre cada um, consulte [Cmdlets do Azure Rights Management](http://msdn.microsoft.com/library/azure/dn629398.aspx).

> [!NOTE]
> Se você precisar instalar o módulo do Windows PowerShell para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], consulte [Instalando o Windows PowerShell para Azure Rights Management](install-powershell.md).

Também existe um módulo complementar do Windows PowerShell, **RMSProtection**, que oferece suporte ao Azure RMS e ao AD RMS. Este módulo é compatível com a proteção e a remoção da proteção de vários arquivos de forma que, por exemplo, você possa proteger em massa todos os arquivos em uma pasta. Para obter mais informações, consulte a seção [Opções de script para superusuários](configure-super-users.md#scripting-options-for-super-users) no artigo [Configurando os superusuários para o Azure Rights Management e os serviços de descoberta ou recuperação de dados](configure-super-users.md).

|Se for necessário...|…use os cmdlets a seguir|
|-------------------|------------------------------|
|Migrar do Rights Management local (AD RMS ou Windows RMS) para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|[Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx)|
|Conecte-se ou desconecte-se do serviço [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para a sua organização.|[Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx)<br /><br />[Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx)|
|Gere e gerencie sua própria chave de locatário (cenário traga sua própria chave (BYOK).|[Add-AadrmKey](http://msdn.microsoft.com/library/azure/dn629418.aspx)<br /><br />[Get-AadrmKeys](http://msdn.microsoft.com/library/azure/dn629420.aspx)|
|Ative ou desative o serviço [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para a sua organização.|[Enable-Aadrm](http://msdn.microsoft.com/library/azure/dn629412.aspx)<br /><br />[Disable-Aadrm](http://msdn.microsoft.com/library/azure/dn629422.aspx)|
|Desabilitar ou habilitar o site de rastreamento de documentos do Azure Rights Management.|[Disable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548471.aspx)<br /><br />[Enable-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548469.aspx)<br /><br />[Get-AadrmDocumentTrackingFeature](https://msdn.microsoft.com/library/azure/mt548470.aspx)|
|Configurar controles de integração para uma implantação em fases do Azure Rights Management.|[Get-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857522.aspx)<br /><br />[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx)|
|Crie e gerencie os modelos de política de direitos para sua organização.|[Add-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727075.aspx)<br /><br />[Expout-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727078.aspx)<br /><br />[Get-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727079.aspx)<br /><br />[Get-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727081.aspx)<br /><br />[Impout-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727077.aspx)<br /><br />[New-AadrmRightsDefinition](http://msdn.microsoft.com/library/azure/dn727080.aspx)<br /><br />[Remove-AadrmTemplate](http://msdn.microsoft.com/library/azure/dn727082.aspx)<br /><br />[Set-AadrmTemplateProperty](http://msdn.microsoft.com/library/azure/dn727076.aspx)|
|Configurar o número máximo de dias em que é possível acessar o conteúdo protegido por sua organização sem uma conexão à Internet (o período de validade da licença de uso).|[Get-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932062.aspx)<br /><br />[Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx)|
|Gerencie o recurso de super-usuário do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para a sua organização.|[Enable-AadrmSuperUserFeature](https://msdn.microsoft.com/library/azure/dn629400.aspx)<br /><br />[Desabilitar-RecursodeSuperusuárioAadrm](https://msdn.microsoft.com/library/azure/dn629428.aspx)<br /><br />[Add-AadrmSuperUser](http://msdn.microsoft.com/library/azure/dn629411.aspx)<br /><br />[Get-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629408.aspx)<br /><br />[Remove-AadrmSuperUser](https://msdn.microsoft.com/library/azure/dn629405.aspx)<br /><br />[Set-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653943.aspx)<br /><br />[Get-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653942.aspx)<br /><br />[Clear-AadrmSuperUserGroup](https://msdn.microsoft.com/library/azure/mt653944.aspx)|
|Gerencie usuários e grupos que estão autorizados a administrar o serviço [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para a sua organização.|[Add-AadrmRoleBasedAdministrator](http://msdn.microsoft.com/library/azure/dn629417.aspx)<br /><br />[Get-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/azure/dn629407.aspx)<br /><br />[Remover-AdministradorAadrmBaseadoemFunção](https://msdn.microsoft.com/library/azure/dn629424.aspx)|
|Obtenha um registro de tarefas administrativas do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para a sua organização.|[Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx)|
|Registre e analise o registro de uso para o [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|[Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx)|
|Exiba a configuração de serviço atual do [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] para a sua organização.|[Get-AadrmConfiguration](http://msdn.microsoft.com/library/azure/dn629410.aspx)|
|Migre a sua organização do [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] para uma implantação do AD RMS local.|[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx)<br /><br />[Get-AadrmMigrationUrl](http://msdn.microsoft.com/library/azure/dn629403.aspx)|





<!--HONumber=Apr16_HO3-->


