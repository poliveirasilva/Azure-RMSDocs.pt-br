---
# required metadata

title: Referência do PowerShell para modelos personalizados | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---



# Referência do PowerShell para modelos personalizados

*Aplica-se a: Azure Rights Management, Office 365*

Tudo o que consegue fazer no portal clássico do Azure para criar e gerir modelos, pode fazer a partir da linha de comandos com o PowerShell. Além disso, pode exportar e importar modelos para poder copiar modelos entre inquilinos ou fazer edições em volume de propriedades complexas nos modelos, como nomes e descrições multilingues.

Também pode utilizar a exportação e importação para criar uma cópia de segurança e restaurar os modelos personalizados. De acordo com as melhores práticas, crie uma cópia de segurança dos seus modelos personalizados regularmente, pois se fizer uma alteração que não pretendia, pode facilmente reverter para uma versão anterior.

> [!IMPORTANT] Para utilizar o Windows PowerShell para criar e gerir modelos de política de direitos do Azure RMS, tem de ter, pelo menos, a versão 2.0.0.0 do [módulo do Windows PowerShell para o Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Se já tiver instalado este módulo do PowerShell, execute o seguinte comando numa janela do PowerShell para verificar o número da versão: `(Get-Module aadrm -ListAvailable).Version`

Para obter instruções de instalação, consulte [Installing Windows PowerShell for Azure Rights Management (Instalar o Windows PowerShell para o Azure Rights Management – em inglês)](install-powershell.md).

Os cmdlets que suportam a criação e gestão de modelos:

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)



## Consulte Também
[Configurar modelos personalizados para o Azure Rights Management](configure-custom-templates.md)

<!--HONumber=May16_HO3-->


