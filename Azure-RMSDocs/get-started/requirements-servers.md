---
# required metadata

title: Requisitos do Azure RMS&#58; Servidores locais que dão suporte ao Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Requisitos do Azure RMS: servidores locais que dão suporte ao Azure RMS
Os seguintes produtos de servidor local são suportados com o Azure RMS ao usar o conector Azure RMS, que atua como uma interface de comunicação entre os servidores locais e o Azure RMS (um retransmissor). Além disso, essa configuração requer uma configuração da sincronização de diretório entre as florestas do Active Directory e do Azure Active Directory.

-   **Exchange Server**:

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Servidores de arquivos que executam o Windows Server e usam a FCI (Infraestrutura de Classificação de Arquivos)**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Como os servidores de arquivo que executam o Windows Server 2008 R2 não têm uma ação de tarefa de gerenciamento de arquivos interna para aplicar a proteção RMS, você não pode usar o conector RMS para esse cenário. No entanto, você pode usar a Infraestrutura de Classificação de Arquivos e o Azure RMS nesses sistemas operacionais se você configurar uma tarefa de gerenciamento de arquivos personalizada para executar um script ou executável que podem proteger arquivos usando o Azure RMS. Por exemplo, um script do Windows PowerShell que usa os [cmdlets de proteção RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > Você também pode usar esses cmdlets com servidores que executam versões posteriores do Windows Server, com o benefício de que esses cmdlets conseguem proteger todos os tipos de arquivo. O conector RMS protege apenas arquivos do Office. Para obter instruções, consulte [Proteção RMS com a Infraestrutura de Classificação de Arquivos do Windows Server&#40;FCI&#41;](../rms-client/configure-fci.md).

O conector RMS tem suporte no Windows Server 2012 R2, no Windows Server 2012 e no Windows Server 2008 R2.

Para obter mais informações sobre como configurar o conector RMS para esses servidores locais, consulte [Implantando o conector do Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Próximas etapas
Para verificar se há outros requisitos, consulte [Requisitos do Azure Rights Management](requirements-azure-rms.md).


<!--HONumber=Apr16_HO3-->


