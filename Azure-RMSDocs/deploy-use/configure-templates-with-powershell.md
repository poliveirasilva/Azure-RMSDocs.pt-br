---
title: "Referência do PowerShell para modelos personalizados | Azure RMS"
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
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: 645f9ed4080e3b38fcda9afe148923c021046724


---



# Referência do PowerShell para modelos personalizados

*Aplica-se a: Azure Rights Management, Office 365*

Tudo que você pode fazer no portal clássico do Azure para criar e gerenciar modelos, você pode fazer na linha de comando pelo uso do PowerShell. Além disso, você pode exportar e importar modelos, de modo que você possa copiar os modelos entre locatários ou realizar edições em massa de propriedades complexas em modelos, como nomes e descrições.

Você pode também usar a exportação e importação para fazer backup e restaurar seus modelos personalizados, como melhor prática, fazer backup regularmente de seus modelos personalizados, para que, se você fizer uma alteração não pretendida, poderá revertê-la facilmente para uma versão anterior.

> [!IMPORTANT]
> Para usar o Windows PowerShell para criar e gerenciar modelos de política de direitos do Azure RMS, você deve ter pelo menos a versão 2.0.0.0 do [módulo Windows PowerShell para Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Se você instalou este módulo do PowerShell anteriormente, execute o seguinte comando em uma janela do PowerShell para verificar o número de versão: `(Get-Module aadrm -ListAvailable).Version`

Para instruções de instalação, consulte [Instalando o Windows PowerShell para Azure Rights Management](install-powershell.md).

Os cmdlets que oferecem suporte à criação e gerenciamento de modelos são:

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Expout-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Impout-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)



## Consulte também
[Configurar modelos personalizados do Azure Rights Management](configure-custom-templates.md)


<!--HONumber=Jul16_HO3-->


