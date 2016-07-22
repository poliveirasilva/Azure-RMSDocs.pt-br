---
title: "Servidores de ficheiros que executam o Windows Server e utilizam a Infraestrutura de Classificação de Ficheiros (FCI) | Azure RMS"
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


# Servidores de ficheiros que executam o Windows Server e utilizam a Infraestrutura de Classificação de Ficheiros (FCI)

*Aplica-se a: Azure Rights Management, Office 365*


Quando configura o Windows Server para utilizar a Infraestrutura de Classificação de Ficheiros, esta funcionalidade do Gestor de Recursos de Servidor de Ficheiros pode analisar ficheiros locais e determinar se contêm dados sensíveis. Os ficheiros que obedecem a estes critérios são etiquetados com propriedades de classificação definidas por um administrador. A Infraestrutura de Classificação de Ficheiros pode então tomar uma ação automática, de acordo com a classificação. Uma destas ações inclui aplicar proteção de informações ao utilizar o [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] e a implementação do conector Rights Management (também conhecido como conector RMS). Os ficheiros do Office são então automaticamente protegidos pelo Azure RMS.

Para proteger todos os tipos de ficheiros, não deverá utilizar o conector RMS, em vez disso, deverá executar um script do Windows PowerShell, utilizando os cmdlets da [Ferramenta de Proteção RMS](https://www.microsoft.com/en-us/download/details.aspx?id=47256).

As políticas de classificação são totalmente configuráveis e altamente extensíveis para que possa impedir potenciais fugas de dados de utilizadores autorizados e não autorizados. Podem inclusivamente ajudar a reduzir o risco de fuga de dados por administradores de rede, porque pode configurar políticas que não exijam que estes administradores tenham acesso aos ficheiros.

Para obter instruções para implementar e configurar o conector RMS para ficheiros do Office, consulte [Implementar o conector Azure Rights Management](../deploy-use/deploy-rms-connector.md).

Para obter instruções para utilizar o script do Windows PowerShell para todos os tipos de ficheiros, consulte [Proteção RMS com Infraestrutura de Classificação de Ficheiros &#40;FCI&#41; do Windows Server](../rms-client/configure-fci.md).



## Passos seguintes
Agora que compreende como as aplicações e os serviços suportam o Azure RMS, pode estar interessado em comparar o Azure RMS com a versão no local do Rights Management, os Serviços de Gestão de Direitos do Active Directory (AD RMS). Para obter uma comparação de funcionalidades, requisitos e controlos de segurança, consulte [Comparar o Azure Rights Management e o AD RMS](compare-azure-rms-ad-rms.md).





<!--HONumber=Jun16_HO4-->


