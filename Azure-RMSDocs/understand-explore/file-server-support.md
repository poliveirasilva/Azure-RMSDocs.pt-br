---
title: "Servidores de arquivos que executam o Windows Server e usam a FCI (Infraestrutura de Classificação de Arquivos) | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 839be5a8a45c2322127694dc0bdc306ff445c314


---


# Servidores de arquivos que executam o Windows Server e usam o File Classification Infrastructure (FCI)

*Aplica-se a: Azure Rights Management, Office 365*


Ao configurar o Windows Server para usar o File Classification Infrastructure, este recurso de Gerenciador de Recursos do Servidor de Arquivos pode verificar os arquivos e determinar se eles contêm dados confidenciais. Os arquivos que atendem a esse critério são marcados com propriedades de classificação definidas por um administrador. O File Classification Infrastructure poderá então agir de forma automática, de acordo com a classificação. Uma dessas ações inclui aplicar proteção de informações usando [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] e a implantação do conector Rights Management (também conhecido como conector RMS). Os arquivos do Office serão então automaticamente protegidos pelo Azure RMS.

Para proteger todos os tipos de arquivo, não use o conector RMS, mas, em vez disso, execute um script do Windows PowerShell, usando os cmdlets da [ferramenta de proteção do RMS](https://www.microsoft.com/en-us/download/details.aspx?id=47256).

As políticas de classificação são totalmente configuráveis ​​e altamente extensíveis para que você possa evitar possíveis vazamentos de dados de usuários não autorizados e autorizados. Elas também podem ajudar a reduzir o risco de vazamento de dados por administradores de rede, pois você pode configurar políticas que não exigem que esses administradores tenham acesso aos arquivos.

Para instruções de como implantar e configurar o conector RMS para arquivos do Office, consulte [Implantando o conector Azure Rights Management](../deploy-use/deploy-rms-connector.md).

Para obter instruções para usar o script do Windows PowerShell para todos os tipos de arquivo, consulte [Proteção RMS com a Infraestrutura de Classificação de Arquivos do Windows Server &#40;FCI&#41;](../rms-client/configure-fci.md).



## Próximas etapas
Se você sabe como os aplicativos e serviços dão suporte ao Azure RMS, talvez tenha interesse em comparar o Azure RMS com a versão local do Rights Management, Active Directory Rights Management Services (AD RMS). Para obter uma comparação de recursos, requisitos e controles de segurança, consulte [Comparando o Azure Rights Management e o AD RMS](compare-azure-rms-ad-rms.md).





<!--HONumber=Jun16_HO4-->


