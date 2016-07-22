---
title: Requisitos do Azure RMS&#58; servidores no local que suportem o Azure Rights Management | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ed50d87138c428fadfd22cd5b3ef3c7f7e421848
ms.openlocfilehash: 7e718d8178dd7c4b18ea7a19eb3165ee06dc4b36


---


# Requisitos do Azure RMS: servidores no local que suportem o Azure Rights Management

*Aplica-se a: Azure Rights Management, Office 365*

Os seguintes produtos de servidor no local são suportados com o Azure RMS quando utiliza o conector Azure RMS, que funciona como uma interface de comunicações (um reencaminhamento) entre os servidores no local e o Azure RMS. Além disso, esta configuração requer que configure a sincronização de diretórios entre as suas florestas do Active Directory e o Azure Active Directory.

-   **Exchange Server**:

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Servidores de ficheiros que executam o Windows Server e utilizam a Infraestrutura de Classificação de Ficheiros (FCI)**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Uma vez que os servidores de ficheiros que executam o Windows Server 2008 R2 não têm uma ação de tarefa de gestão de ficheiros incorporados para aplicar a proteção do RMS, não é possível utilizar o conector RMS para este cenário. No entanto, pode utilizar a Infraestrutura de Classificação de Ficheiros e o Azure RMS nestes sistemas operativos se configurar uma tarefa de gestão de ficheiros personalizada para executar um executável ou um script que possa proteger ficheiros ao utilizar o Azure RMS. Por exemplo, um script do Windows PowerShell que utiliza os [Cmdlets de Proteção RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > Também pode utilizar estes cmdlets com servidores a executar versões posteriores do Windows Server, com a vantagem de estes cmdlets poderem proteger todos os tipos de ficheiro. O conector RMS protege apenas os ficheiros do Office. Para obter instruções sobre como utilizar, consulte [Proteção RMS com Infraestrutura de Classificação de Ficheiros do Windows Server &#40;FCI&#41;](../rms-client/configure-fci.md).

O conector RMS é suportado no Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2.

Para obter mais informações acerca de como configurar o conetor RMS para estes servidores no local, consulte [Implementar o conetor do Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Passos seguintes
Para verificar outros requisitos, consulte [Requisitos do Azure Rights Management](requirements-azure-rms.md).



<!--HONumber=Jun16_HO4-->


