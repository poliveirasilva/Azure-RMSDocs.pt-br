---
title: Termos | Azure RMS
description: "Uma coleção de definições de terminologia específicas do Rights Management Services."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: adb1f868-0da7-431b-83d1-86f41c2da4ae
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: 5779cc10503ad7afe997e031a467021b513fc510


---

# Termos

Uma coleção de definições de terminologia específicas do Rights Management Services.

**Algoritmo preterido**  
Uma configuração modal que implementa um esquema de proteção de conteúdo mais antigo, referindo-se especificamente ao modo de criptografia ECB (guia eletrônico). Nesse SDK, a configuração permite que você gere licenças compatíveis com a biblioteca MSDRM usada pelo [AD Rights Management Services SDK](https://msdn.microsoft.com/library/windows/desktop/cc530379.aspx).

Essa configuração pode fazer seu aplicativo proteger o conteúdo de uma maneira que não esteja em conformidade com os padrões de seus clientes para proteção de conteúdo.

Essa configuração impedirá que seu aplicativo se beneficie de quaisquer aperfeiçoamentos de criptografia adicionados ao Microsoft Rights Management SDK 3.0 ou posterior.

**Formato de arquivo protegido da Microsoft**

Também conhecido como formato PFile, é o formato de arquivo padrão para o AD RMS e funções como um padrão em todos os aplicativos habilitados para RMS.

O formato de arquivo PFile é transparente para o desenvolvedor do aplicativo conforme ele é incorporado na maneira como o Microsoft Rights Management SDK 4.2 é projetado.

 

 






<!--HONumber=Jul16_HO2-->


